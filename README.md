# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-21T07:56:56Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.24K | ± 1.96K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.95K | ± 38.19 | ops/s | 1.1x slower |
| prometheusAdd | 48.70K | ± 316.08 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.51K | ± 283.07 | ops/s | 1.3x slower |
| simpleclientInc | 6.05K | ± 44.21 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 5.86K | ± 49.32 | ops/s | 9.9x slower |
| simpleclientAdd | 5.75K | ± 119.01 | ops/s | 10x slower |
| openTelemetryAdd | 1.35K | ± 10.21 | ops/s | 43x slower |
| openTelemetryInc | 1.31K | ± 48.83 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.31K | ± 107.47 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.57K | ± 388.40 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 56.84 | ops/s | 1.0x slower |
| prometheusNative | 2.99K | ± 239.41 | ops/s | 1.5x slower |
| openTelemetryClassic | 623.94 | ± 30.13 | ops/s | 7.3x slower |
| openTelemetryExponential | 526.58 | ± 23.65 | ops/s | 8.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 549.72K | ± 1.65K | ops/s | **fastest** |
| prometheusWriteToByteArray | 542.46K | ± 6.20K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 532.55K | ± 6.78K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 520.76K | ± 3.04K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44511.305    ± 283.074  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1352.352     ± 10.206  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1311.977     ± 48.827  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1306.476    ± 107.467  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48703.069    ± 316.079  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58238.131   ± 1964.034  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50950.587     ± 38.193  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5753.268    ± 119.014  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6048.249     ± 44.214  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5860.270     ± 49.324  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        623.935     ± 30.129  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        526.579     ± 23.652  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4568.649    ± 388.396  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2985.774    ± 239.410  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4416.903     ± 56.843  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     520763.839   ± 3039.086  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     532549.957   ± 6783.173  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     542460.761   ± 6201.691  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     549724.565   ± 1648.271  ops/s
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
