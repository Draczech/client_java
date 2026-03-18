# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-18T05:28:39Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.27K | ± 190.96 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.50K | ± 684.18 | ops/s | 1.2x slower |
| prometheusAdd | 51.65K | ± 230.97 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.08K | ± 1.76K | ops/s | 1.4x slower |
| simpleclientInc | 6.52K | ± 180.69 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.52K | ± 140.91 | ops/s | 10x slower |
| simpleclientAdd | 6.27K | ± 170.03 | ops/s | 11x slower |
| openTelemetryInc | 1.26K | ± 31.65 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.26K | ± 14.70 | ops/s | 53x slower |
| openTelemetryAdd | 1.23K | ± 5.09 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.15K | ± 1.07K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 34.18 | ops/s | 1.1x slower |
| prometheusNative | 2.98K | ± 303.62 | ops/s | 1.7x slower |
| openTelemetryClassic | 699.92 | ± 12.95 | ops/s | 7.4x slower |
| openTelemetryExponential | 578.81 | ± 8.53 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 485.06K | ± 8.43K | ops/s | **fastest** |
| openMetricsWriteToByteArray | 482.09K | ± 9.35K | ops/s | 1.0x slower |
| prometheusWriteToNull | 475.69K | ± 1.97K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 467.32K | ± 19.26K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49080.181   ± 1760.610  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1233.673      ± 5.094  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1264.026     ± 31.646  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1259.252     ± 14.699  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51645.279    ± 230.967  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66265.323    ± 190.955  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56499.290    ± 684.183  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6269.979    ± 170.029  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6523.999    ± 180.691  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6521.790    ± 140.906  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        699.921     ± 12.951  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        578.815      ± 8.525  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5149.424   ± 1071.947  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2979.406    ± 303.616  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4541.761     ± 34.182  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482088.589   ± 9353.789  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     467318.212  ± 19258.573  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485059.026   ± 8430.406  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     475690.562   ± 1969.620  ops/s
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
