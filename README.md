# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-21T05:10:32Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.35K | ± 2.53K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.25K | ± 946.65 | ops/s | 1.1x slower |
| prometheusAdd | 51.03K | ± 645.51 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.04K | ± 1.04K | ops/s | 1.3x slower |
| simpleclientInc | 6.64K | ± 132.86 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.56K | ± 204.44 | ops/s | 9.8x slower |
| simpleclientAdd | 6.35K | ± 162.07 | ops/s | 10x slower |
| openTelemetryAdd | 1.39K | ± 238.62 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.37K | ± 232.26 | ops/s | 47x slower |
| openTelemetryInc | 1.31K | ± 87.27 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.28K | ± 1.98K | ops/s | **fastest** |
| simpleclient | 4.57K | ± 53.89 | ops/s | 1.6x slower |
| prometheusNative | 2.88K | ± 161.53 | ops/s | 2.5x slower |
| openTelemetryClassic | 691.60 | ± 28.42 | ops/s | 11x slower |
| openTelemetryExponential | 550.86 | ± 12.38 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.59K | ± 2.42K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.55K | ± 7.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.16K | ± 3.58K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.58K | ± 3.76K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48041.364   ± 1041.296  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1390.345    ± 238.621  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1308.961     ± 87.269  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1374.463    ± 232.261  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51026.015    ± 645.512  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64348.509   ± 2531.168  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56249.391    ± 946.654  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6349.563    ± 162.071  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6644.784    ± 132.859  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6561.141    ± 204.439  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.597     ± 28.417  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.861     ± 12.381  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7280.955   ± 1981.186  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2875.636    ± 161.534  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4567.056     ± 53.888  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475581.919   ± 3756.111  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486160.054   ± 3577.949  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488551.097   ± 7234.817  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492586.706   ± 2415.136  ops/s
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
