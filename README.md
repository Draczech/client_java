# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-01T09:10:44Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.31K | ± 1.38K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.84K | ± 278.75 | ops/s | 1.1x slower |
| prometheusAdd | 51.47K | ± 363.68 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.54K | ± 2.04K | ops/s | 1.3x slower |
| simpleclientInc | 6.64K | ± 53.32 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.50K | ± 196.05 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 253.65 | ops/s | 10x slower |
| openTelemetryAdd | 1.48K | ± 157.75 | ops/s | 44x slower |
| openTelemetryInc | 1.40K | ± 214.15 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.24K | ± 38.76 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.53K | ± 1.61K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 85.69 | ops/s | 1.3x slower |
| prometheusNative | 2.74K | ± 435.84 | ops/s | 2.0x slower |
| openTelemetryClassic | 712.87 | ± 13.53 | ops/s | 7.8x slower |
| openTelemetryExponential | 549.96 | ± 40.50 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.08K | ± 2.65K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.82K | ± 1.81K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.56K | ± 3.54K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.38K | ± 5.84K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49542.314   ± 2036.441  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1477.428    ± 157.754  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1395.751    ± 214.153  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1237.377     ± 38.761  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51474.064    ± 363.678  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65311.549   ± 1380.582  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56843.092    ± 278.747  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6320.457    ± 253.654  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6641.671     ± 53.317  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6498.151    ± 196.054  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        712.870     ± 13.531  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        549.964     ± 40.500  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5528.744   ± 1611.480  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2737.621    ± 435.839  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4415.922     ± 85.686  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467377.845   ± 5842.068  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478559.830   ± 3540.668  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480817.751   ± 1809.013  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485078.516   ± 2654.019  ops/s
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
