# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-26T04:11:27Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 67.88K | ± 873.36 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.61K | ± 2.61K | ops/s | 1.2x slower |
| prometheusAdd | 50.63K | ± 1.93K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.49K | ± 1.64K | ops/s | 1.4x slower |
| simpleclientInc | 6.77K | ± 141.05 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.51K | ± 217.01 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 195.12 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.36K | ± 216.30 | ops/s | 50x slower |
| openTelemetryInc | 1.32K | ± 20.88 | ops/s | 52x slower |
| openTelemetryAdd | 1.28K | ± 22.22 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.81K | ± 1.04K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 83.12 | ops/s | 1.3x slower |
| prometheusNative | 2.96K | ± 259.32 | ops/s | 2.0x slower |
| openTelemetryClassic | 675.79 | ± 26.89 | ops/s | 8.6x slower |
| openTelemetryExponential | 587.32 | ± 12.37 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.72K | ± 6.40K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.58K | ± 3.95K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 485.30K | ± 8.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.72K | ± 7.32K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49490.739   ± 1641.646  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1275.669     ± 22.220  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1315.118     ± 20.876  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1359.647    ± 216.298  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50625.865   ± 1933.265  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      67883.257    ± 873.356  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56613.980   ± 2606.648  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6459.753    ± 195.118  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6767.226    ± 141.046  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6506.398    ± 217.006  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        675.794     ± 26.892  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        587.322     ± 12.371  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5807.010   ± 1041.471  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2962.056    ± 259.323  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4514.172     ± 83.115  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485299.143   ± 8549.254  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478715.440   ± 7324.883  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488582.578   ± 3950.659  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493719.820   ± 6402.554  ops/s
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
