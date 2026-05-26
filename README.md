# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-26T07:13:32Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.09K | ± 3.82K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.71K | ± 65.28 | ops/s | 1.1x slower |
| prometheusAdd | 48.31K | ± 1.11K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.99K | ± 774.78 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.20K | ± 31.44 | ops/s | 9.2x slower |
| simpleclientInc | 6.18K | ± 93.43 | ops/s | 9.2x slower |
| simpleclientAdd | 5.67K | ± 132.66 | ops/s | 10x slower |
| openTelemetryInc | 1.49K | ± 80.18 | ops/s | 38x slower |
| openTelemetryAdd | 1.45K | ± 43.75 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.33K | ± 62.91 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.40K | ± 427.83 | ops/s | **fastest** |
| simpleclient | 4.28K | ± 146.66 | ops/s | 1.0x slower |
| prometheusNative | 2.91K | ± 188.11 | ops/s | 1.5x slower |
| openTelemetryClassic | 607.38 | ± 22.57 | ops/s | 7.2x slower |
| openTelemetryExponential | 523.79 | ± 10.91 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 552.08K | ± 6.99K | ops/s | **fastest** |
| prometheusWriteToByteArray | 544.01K | ± 5.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 537.13K | ± 7.60K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 525.19K | ± 8.85K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43992.482    ± 774.775  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1445.033     ± 43.750  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1486.971     ± 80.182  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1329.112     ± 62.905  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48311.056   ± 1106.721  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57085.494   ± 3819.892  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51705.289     ± 65.275  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5668.964    ± 132.663  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6180.967     ± 93.429  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6200.149     ± 31.437  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        607.382     ± 22.572  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        523.788     ± 10.914  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4400.227    ± 427.832  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2906.884    ± 188.113  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4283.187    ± 146.660  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     525188.581   ± 8849.874  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     537132.171   ± 7597.734  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     544005.769   ± 5081.443  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     552079.768   ± 6991.604  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
