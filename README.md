# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-13T06:38:15Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.22K | ± 616.93 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.65K | ± 780.99 | ops/s | 1.2x slower |
| prometheusAdd | 51.35K | ± 167.28 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.27K | ± 1.51K | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 69.82 | ops/s | 9.9x slower |
| simpleclientAdd | 6.44K | ± 37.20 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.42K | ± 193.40 | ops/s | 10x slower |
| openTelemetryInc | 1.46K | ± 206.85 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.31K | ± 92.08 | ops/s | 50x slower |
| openTelemetryAdd | 1.27K | ± 12.95 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.62K | ± 837.77 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 54.42 | ops/s | 1.5x slower |
| prometheusNative | 3.01K | ± 286.88 | ops/s | 2.2x slower |
| openTelemetryClassic | 727.89 | ± 14.36 | ops/s | 9.1x slower |
| openTelemetryExponential | 561.05 | ± 7.52 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.79K | ± 2.02K | ops/s | **fastest** |
| openMetricsWriteToNull | 484.62K | ± 3.78K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 481.79K | ± 4.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.69K | ± 6.28K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48269.999   ± 1506.371  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1270.401     ± 12.951  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1458.512    ± 206.846  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1311.856     ± 92.078  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51354.875    ± 167.278  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66221.879    ± 616.927  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56651.863    ± 780.989  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6443.890     ± 37.200  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6656.935     ± 69.817  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6416.391    ± 193.397  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        727.892     ± 14.363  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.049      ± 7.519  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6616.604    ± 837.772  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3011.170    ± 286.879  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4405.898     ± 54.415  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475689.773   ± 6278.200  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484616.545   ± 3777.288  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481794.147   ± 4468.929  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490793.614   ± 2023.835  ops/s
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
