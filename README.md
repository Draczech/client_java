# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-01T08:09:37Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.84K | ± 774.16 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.62K | ± 42.91 | ops/s | 1.2x slower |
| prometheusAdd | 47.86K | ± 456.62 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 42.05K | ± 3.13K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.30K | ± 6.01 | ops/s | 9.7x slower |
| simpleclientInc | 6.25K | ± 141.27 | ops/s | 9.7x slower |
| simpleclientAdd | 5.90K | ± 222.97 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.51K | ± 138.16 | ops/s | 40x slower |
| openTelemetryAdd | 1.46K | ± 119.17 | ops/s | 42x slower |
| openTelemetryInc | 1.42K | ± 119.95 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.92K | ± 358.76 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 56.30 | ops/s | 1.1x slower |
| prometheusNative | 2.89K | ± 182.05 | ops/s | 1.7x slower |
| openTelemetryClassic | 631.85 | ± 14.39 | ops/s | 7.8x slower |
| openTelemetryExponential | 539.77 | ± 16.56 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 558.49K | ± 4.54K | ops/s | **fastest** |
| prometheusWriteToByteArray | 539.01K | ± 3.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 532.32K | ± 6.49K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.06K | ± 2.42K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42052.148   ± 3129.383  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1456.642    ± 119.165  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1420.024    ± 119.952  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1505.093    ± 138.164  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47857.410    ± 456.619  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60844.565    ± 774.160  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52618.169     ± 42.914  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5904.524    ± 222.967  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6250.467    ± 141.269  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6302.579      ± 6.014  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        631.849     ± 14.390  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        539.775     ± 16.564  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4919.381    ± 358.763  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2885.292    ± 182.055  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4561.815     ± 56.299  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524058.945   ± 2415.699  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     532322.487   ± 6494.470  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     539012.366   ± 3802.776  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     558490.585   ± 4544.443  ops/s
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
