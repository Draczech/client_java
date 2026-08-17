# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-17T04:06:17Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusAdd | 36.57K | ± 546.31 | ops/s | **fastest** |
| codahaleIncNoLabels | 35.67K | ± 1.75K | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 35.07K | ± 990.76 | ops/s | 1.0x slower |
| prometheusInc | 35.06K | ± 768.50 | ops/s | 1.0x slower |
| simpleclientInc | 9.07K | ± 200.40 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 8.92K | ± 147.21 | ops/s | 4.1x slower |
| simpleclientAdd | 8.60K | ± 239.05 | ops/s | 4.3x slower |
| openTelemetryInc | 917.98 | ± 86.48 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 895.55 | ± 14.59 | ops/s | 41x slower |
| openTelemetryAdd | 818.39 | ± 36.94 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.98K | ± 146.82 | ops/s | **fastest** |
| prometheusClassic | 4.27K | ± 2.12K | ops/s | 1.4x slower |
| prometheusNative | 2.15K | ± 334.57 | ops/s | 2.8x slower |
| openTelemetryClassic | 356.42 | ± 7.09 | ops/s | 17x slower |
| openTelemetryExponential | 320.67 | ± 14.41 | ops/s | 19x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 362.44K | ± 9.00K | ops/s | **fastest** |
| prometheusWriteToByteArray | 354.74K | ± 10.86K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 337.64K | ± 4.50K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 328.93K | ± 9.75K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      35671.960   ± 1752.489  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15        818.390     ± 36.939  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15        917.980     ± 86.480  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15        895.547     ± 14.590  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      36573.737    ± 546.308  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      35058.124    ± 768.505  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      35071.783    ± 990.759  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       8596.289    ± 239.045  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       9074.973    ± 200.404  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8924.435    ± 147.211  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        356.418      ± 7.095  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        320.674     ± 14.410  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4269.377   ± 2124.747  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2153.687    ± 334.568  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5981.591    ± 146.824  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     337639.627   ± 4503.337  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     328932.923   ± 9751.082  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     354743.131  ± 10855.560  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     362441.185   ± 9000.138  ops/s
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
