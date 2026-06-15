# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-15T08:21:48Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.18K | ± 1.14K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.03K | ± 483.14 | ops/s | 1.1x slower |
| prometheusAdd | 50.77K | ± 468.03 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.81K | ± 2.97K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.61K | ± 19.13 | ops/s | 9.7x slower |
| simpleclientInc | 6.37K | ± 14.54 | ops/s | 10x slower |
| simpleclientAdd | 6.01K | ± 156.22 | ops/s | 11x slower |
| openTelemetryAdd | 1.42K | ± 250.94 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.23K | ± 62.42 | ops/s | 52x slower |
| openTelemetryInc | 1.22K | ± 21.30 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.57K | ± 1.02K | ops/s | **fastest** |
| simpleclient | 4.37K | ± 27.14 | ops/s | 1.5x slower |
| prometheusNative | 2.96K | ± 385.31 | ops/s | 2.2x slower |
| openTelemetryClassic | 685.99 | ± 1.25 | ops/s | 9.6x slower |
| openTelemetryExponential | 555.64 | ± 14.45 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.23K | ± 3.77K | ops/s | **fastest** |
| openMetricsWriteToNull | 489.98K | ± 1.89K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 485.31K | ± 6.76K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.53K | ± 6.14K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48813.888   ± 2969.602  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1422.223    ± 250.936  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1219.722     ± 21.303  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1232.559     ± 62.425  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50774.428    ± 468.028  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64182.920   ± 1144.828  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57031.663    ± 483.136  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6009.394    ± 156.219  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6366.519     ± 14.535  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6614.294     ± 19.131  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        685.991      ± 1.248  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        555.637     ± 14.445  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6571.440   ± 1018.017  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2958.272    ± 385.308  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4367.633     ± 27.145  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475529.654   ± 6143.572  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489978.058   ± 1893.673  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485309.272   ± 6760.283  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492228.798   ± 3765.668  ops/s
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
