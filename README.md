# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-30T05:51:11Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.07K | ± 421.65 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.63K | ± 333.11 | ops/s | 1.2x slower |
| prometheusAdd | 51.24K | ± 417.90 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.45K | ± 1.41K | ops/s | 1.4x slower |
| simpleclientInc | 6.67K | ± 59.19 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 179.01 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 279.09 | ops/s | 10x slower |
| openTelemetryAdd | 1.52K | ± 278.71 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.35K | ± 184.59 | ops/s | 49x slower |
| openTelemetryInc | 1.20K | ± 60.15 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.81K | ± 759.97 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 44.73 | ops/s | 1.1x slower |
| prometheusNative | 2.62K | ± 140.27 | ops/s | 1.8x slower |
| openTelemetryClassic | 712.58 | ± 17.40 | ops/s | 6.7x slower |
| openTelemetryExponential | 560.77 | ± 18.64 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.41K | ± 2.20K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.58K | ± 3.20K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 474.01K | ± 3.64K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 465.19K | ± 3.47K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48445.069   ± 1411.769  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1515.577    ± 278.708  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1200.685     ± 60.146  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1348.248    ± 184.594  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51240.490    ± 417.898  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66068.648    ± 421.649  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56632.653    ± 333.107  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6313.606    ± 279.092  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6666.344     ± 59.189  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6481.409    ± 179.010  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        712.580     ± 17.402  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.769     ± 18.645  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4807.398    ± 759.967  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2620.657    ± 140.273  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4415.262     ± 44.729  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     465188.269   ± 3469.083  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474012.139   ± 3642.707  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484584.383   ± 3197.257  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493411.427   ± 2203.697  ops/s
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
