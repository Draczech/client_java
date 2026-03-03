# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-03T05:19:59Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.86K | ± 640.50 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.00K | ± 450.16 | ops/s | 1.2x slower |
| prometheusAdd | 51.27K | ± 411.57 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.21K | ± 1.66K | ops/s | 1.3x slower |
| simpleclientInc | 6.77K | ± 18.95 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.34K | ± 61.32 | ops/s | 10x slower |
| simpleclientAdd | 6.24K | ± 298.18 | ops/s | 11x slower |
| openTelemetryInc | 1.50K | ± 189.61 | ops/s | 44x slower |
| openTelemetryAdd | 1.48K | ± 222.50 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.22K | ± 59.48 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.55K | ± 578.96 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 49.97 | ops/s | 1.0x slower |
| prometheusNative | 3.03K | ± 282.07 | ops/s | 1.5x slower |
| openTelemetryClassic | 676.64 | ± 40.48 | ops/s | 6.7x slower |
| openTelemetryExponential | 527.38 | ± 25.13 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.70K | ± 3.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.51K | ± 2.60K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.80K | ± 6.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.05K | ± 8.71K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49207.842   ± 1664.065  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1479.492    ± 222.499  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1498.323    ± 189.614  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1218.150     ± 59.484  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51267.748    ± 411.569  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65855.891    ± 640.501  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57000.152    ± 450.155  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6237.912    ± 298.180  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6774.428     ± 18.951  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6343.217     ± 61.322  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        676.640     ± 40.483  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        527.380     ± 25.134  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4549.369    ± 578.960  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3033.201    ± 282.070  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4474.951     ± 49.969  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470049.035   ± 8705.060  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476803.353   ± 6940.657  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485507.315   ± 2601.148  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489702.035   ± 3859.087  ops/s
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
