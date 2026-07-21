# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-21T06:11:59Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.60K | ± 442.10 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.15K | ± 180.73 | ops/s | 1.1x slower |
| prometheusAdd | 51.49K | ± 219.93 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.29K | ± 1.26K | ops/s | 1.4x slower |
| simpleclientInc | 6.55K | ± 220.27 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.46K | ± 217.15 | ops/s | 10x slower |
| simpleclientAdd | 6.17K | ± 252.22 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.56K | ± 223.65 | ops/s | 42x slower |
| openTelemetryInc | 1.51K | ± 215.35 | ops/s | 44x slower |
| openTelemetryAdd | 1.24K | ± 18.49 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.22K | ± 1.11K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 69.54 | ops/s | 1.4x slower |
| prometheusNative | 2.96K | ± 336.31 | ops/s | 2.1x slower |
| openTelemetryClassic | 672.17 | ± 31.51 | ops/s | 9.3x slower |
| openTelemetryExponential | 548.29 | ± 18.76 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.38K | ± 1.22K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.25K | ± 3.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.53K | ± 9.77K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.20K | ± 6.22K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46287.169   ± 1257.893  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1244.408     ± 18.486  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1505.565    ± 215.351  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1559.304    ± 223.650  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51494.631    ± 219.931  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65596.569    ± 442.101  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57148.335    ± 180.732  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6165.198    ± 252.221  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6554.344    ± 220.267  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6458.096    ± 217.145  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        672.173     ± 31.507  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.291     ± 18.765  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6220.305   ± 1113.368  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2960.917    ± 336.307  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4421.263     ± 69.544  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476195.169   ± 6223.999  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478525.220   ± 9773.083  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485252.692   ± 3431.206  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490381.470   ± 1219.174  ops/s
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
