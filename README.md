# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-11T07:48:07Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.74K | ± 1.17K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.40K | ± 429.82 | ops/s | 1.1x slower |
| prometheusAdd | 48.22K | ± 386.92 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.36K | ± 221.26 | ops/s | 1.3x slower |
| simpleclientInc | 6.21K | ± 146.31 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 5.96K | ± 273.80 | ops/s | 10x slower |
| simpleclientAdd | 5.83K | ± 24.84 | ops/s | 10x slower |
| openTelemetryInc | 1.35K | ± 83.26 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.26K | ± 15.53 | ops/s | 47x slower |
| openTelemetryAdd | 1.25K | ± 5.17 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.33K | ± 2.02K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 169.92 | ops/s | 1.6x slower |
| prometheusNative | 3.01K | ± 209.50 | ops/s | 2.4x slower |
| openTelemetryClassic | 664.20 | ± 32.25 | ops/s | 11x slower |
| openTelemetryExponential | 526.17 | ± 4.25 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 539.54K | ± 5.70K | ops/s | **fastest** |
| prometheusWriteToByteArray | 517.09K | ± 14.21K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.51K | ± 4.72K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 503.52K | ± 8.83K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44361.805    ± 221.259  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1247.671      ± 5.169  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1353.403     ± 83.258  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1264.790     ± 15.530  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48216.590    ± 386.916  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59738.239   ± 1171.337  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52396.433    ± 429.820  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5830.569     ± 24.836  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6205.730    ± 146.309  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5963.115    ± 273.802  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        664.200     ± 32.252  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        526.171      ± 4.250  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7326.467   ± 2016.272  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3009.714    ± 209.500  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4464.934    ± 169.921  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     503524.458   ± 8831.645  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512510.374   ± 4715.068  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     517089.354  ± 14209.290  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     539543.631   ± 5697.431  ops/s
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
