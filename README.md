# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-08T07:42:38Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.06K | ± 1.16K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.63K | ± 522.87 | ops/s | 1.2x slower |
| prometheusAdd | 48.78K | ± 623.12 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.50K | ± 576.34 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.28K | ± 34.14 | ops/s | 9.6x slower |
| simpleclientInc | 6.22K | ± 218.73 | ops/s | 9.7x slower |
| simpleclientAdd | 6.07K | ± 196.81 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.47K | ± 95.76 | ops/s | 41x slower |
| openTelemetryAdd | 1.42K | ± 26.97 | ops/s | 42x slower |
| openTelemetryInc | 1.34K | ± 63.55 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.78K | ± 504.47 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 92.06 | ops/s | 1.1x slower |
| prometheusNative | 2.99K | ± 251.88 | ops/s | 1.6x slower |
| openTelemetryClassic | 630.23 | ± 42.23 | ops/s | 7.6x slower |
| openTelemetryExponential | 559.06 | ± 18.85 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.13K | ± 4.61K | ops/s | **fastest** |
| prometheusWriteToByteArray | 549.56K | ± 1.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 536.33K | ± 1.77K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 526.27K | ± 5.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44495.281    ± 576.336  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1418.127     ± 26.971  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1340.350     ± 63.551  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1465.267     ± 95.756  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48782.583    ± 623.123  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60060.337   ± 1158.897  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51625.921    ± 522.873  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6065.159    ± 196.815  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6221.072    ± 218.730  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6278.753     ± 34.141  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        630.232     ± 42.231  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.065     ± 18.848  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4775.259    ± 504.467  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2994.716    ± 251.883  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4538.211     ± 92.063  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     526269.176   ± 5289.528  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     536325.679   ± 1773.016  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     549560.428   ± 1819.248  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555129.639   ± 4614.798  ops/s
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
