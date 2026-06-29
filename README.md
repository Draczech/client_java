# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-29T07:42:17Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.30K | ± 2.49K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.37K | ± 1.75K | ops/s | 1.2x slower |
| prometheusAdd | 48.37K | ± 1.01K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.90K | ± 35.25 | ops/s | 1.3x slower |
| simpleclientInc | 6.23K | ± 153.77 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.13K | ± 200.12 | ops/s | 9.5x slower |
| simpleclientAdd | 6.12K | ± 66.00 | ops/s | 9.5x slower |
| openTelemetryAdd | 1.34K | ± 75.24 | ops/s | 44x slower |
| openTelemetryInc | 1.33K | ± 118.39 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.32K | ± 162.22 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.27K | ± 1.71K | ops/s | **fastest** |
| simpleclient | 4.25K | ± 154.78 | ops/s | 1.2x slower |
| prometheusNative | 3.06K | ± 150.68 | ops/s | 1.7x slower |
| openTelemetryClassic | 612.52 | ± 15.03 | ops/s | 8.6x slower |
| openTelemetryExponential | 530.22 | ± 15.74 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.89K | ± 4.99K | ops/s | **fastest** |
| prometheusWriteToByteArray | 547.73K | ± 8.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 540.76K | ± 5.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 529.52K | ± 4.46K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43896.983     ± 35.246  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1340.039     ± 75.244  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1330.189    ± 118.389  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1322.376    ± 162.222  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48374.418   ± 1014.519  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58296.103   ± 2489.163  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50369.001   ± 1748.419  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6115.797     ± 66.001  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6225.983    ± 153.766  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6133.751    ± 200.123  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        612.518     ± 15.030  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        530.215     ± 15.744  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5274.928   ± 1711.234  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3057.216    ± 150.685  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4251.579    ± 154.782  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     529518.489   ± 4455.118  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     540762.400   ± 5304.920  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     547731.375   ± 8132.589  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555891.880   ± 4985.436  ops/s
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
