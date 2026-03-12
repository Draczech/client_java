# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-12T05:19:40Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.59K | ± 48.24 | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.49K | ± 883.35 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 29.09K | ± 377.31 | ops/s | 1.1x slower |
| prometheusAdd | 28.50K | ± 14.43 | ops/s | 1.1x slower |
| simpleclientInc | 6.97K | ± 138.45 | ops/s | 4.5x slower |
| simpleclientAdd | 6.71K | ± 180.64 | ops/s | 4.7x slower |
| simpleclientNoLabelsInc | 6.70K | ± 269.99 | ops/s | 4.7x slower |
| openTelemetryIncNoLabels | 1.47K | ± 33.04 | ops/s | 21x slower |
| openTelemetryInc | 1.35K | ± 113.93 | ops/s | 23x slower |
| openTelemetryAdd | 1.33K | ± 82.30 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.57K | ± 38.25 | ops/s | **fastest** |
| prometheusClassic | 3.33K | ± 420.17 | ops/s | 1.4x slower |
| prometheusNative | 2.08K | ± 196.71 | ops/s | 2.2x slower |
| openTelemetryClassic | 480.06 | ± 3.85 | ops/s | 9.5x slower |
| openTelemetryExponential | 404.31 | ± 11.48 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 317.85K | ± 1.74K | ops/s | **fastest** |
| prometheusWriteToByteArray | 313.77K | ± 2.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 298.39K | ± 1.22K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 296.43K | ± 2.41K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29087.477    ± 377.310  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1329.475     ± 82.305  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1354.803    ± 113.925  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1474.289     ± 33.045  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28504.024     ± 14.433  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31593.061     ± 48.240  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29487.016    ± 883.349  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6710.062    ± 180.638  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6967.877    ± 138.454  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6700.637    ± 269.988  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        480.061      ± 3.845  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        404.314     ± 11.482  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3332.344    ± 420.172  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2083.396    ± 196.711  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4573.154     ± 38.252  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     296434.765   ± 2405.199  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     298391.703   ± 1222.713  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     313773.075   ± 2125.095  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     317851.514   ± 1744.809  ops/s
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
