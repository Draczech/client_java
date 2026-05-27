# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-27T07:22:50Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.94K | ± 290.29 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.88K | ± 137.13 | ops/s | 1.2x slower |
| prometheusAdd | 47.49K | ± 464.24 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.27K | ± 897.08 | ops/s | 1.3x slower |
| simpleclientInc | 6.16K | ± 121.31 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.14K | ± 165.36 | ops/s | 9.6x slower |
| simpleclientAdd | 5.94K | ± 183.65 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.51K | ± 68.94 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.38K | ± 57.85 | ops/s | 43x slower |
| openTelemetryInc | 1.37K | ± 15.56 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.80K | ± 1.84K | ops/s | **fastest** |
| simpleclient | 4.34K | ± 52.24 | ops/s | 1.6x slower |
| prometheusNative | 3.02K | ± 268.75 | ops/s | 2.3x slower |
| openTelemetryClassic | 651.39 | ± 16.82 | ops/s | 10x slower |
| openTelemetryExponential | 537.69 | ± 25.99 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.10K | ± 5.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 545.63K | ± 10.91K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.63K | ± 3.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 526.13K | ± 5.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44272.780    ± 897.077  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1508.294     ± 68.943  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1368.798     ± 15.556  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1384.921     ± 57.855  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47487.124    ± 464.239  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58937.026    ± 290.291  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50881.894    ± 137.125  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5935.730    ± 183.645  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6156.937    ± 121.309  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6135.846    ± 165.359  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        651.390     ± 16.819  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        537.695     ± 25.985  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6802.557   ± 1838.301  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3017.617    ± 268.753  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4342.652     ± 52.235  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     526128.544   ± 5063.884  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538627.573   ± 3809.631  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     545627.081  ± 10910.371  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555103.200   ± 5303.536  ops/s
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
