# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-06T07:51:05Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.29K | ± 524.22 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.06K | ± 112.78 | ops/s | 1.2x slower |
| prometheusAdd | 51.27K | ± 378.27 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 45.40K | ± 5.82K | ops/s | 1.5x slower |
| simpleclientInc | 6.59K | ± 152.07 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.27K | ± 65.98 | ops/s | 11x slower |
| simpleclientAdd | 6.17K | ± 232.50 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.37K | ± 138.19 | ops/s | 48x slower |
| openTelemetryInc | 1.33K | ± 92.98 | ops/s | 50x slower |
| openTelemetryAdd | 1.22K | ± 23.51 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.88K | ± 2.04K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 40.31 | ops/s | 1.5x slower |
| prometheusNative | 2.85K | ± 315.90 | ops/s | 2.4x slower |
| openTelemetryClassic | 673.38 | ± 34.71 | ops/s | 10x slower |
| openTelemetryExponential | 566.36 | ± 62.56 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.17K | ± 3.22K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.17K | ± 4.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.54K | ± 2.39K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 461.87K | ± 3.15K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45400.268   ± 5820.984  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1218.776     ± 23.511  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1326.218     ± 92.978  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1368.472    ± 138.186  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51274.058    ± 378.273  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66294.005    ± 524.216  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57056.608    ± 112.785  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6167.612    ± 232.496  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6587.904    ± 152.066  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6271.380     ± 65.984  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        673.375     ± 34.708  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.356     ± 62.557  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6883.655   ± 2036.963  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2845.503    ± 315.898  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4453.493     ± 40.313  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     461871.859   ± 3147.648  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471538.655   ± 2391.756  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480171.475   ± 4126.450  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486169.880   ± 3222.479  ops/s
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
