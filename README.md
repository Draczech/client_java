# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-10T05:14:27Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.58K | ± 58.88 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.04K | ± 176.35 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.97K | ± 658.76 | ops/s | 1.1x slower |
| prometheusAdd | 28.61K | ± 266.49 | ops/s | 1.1x slower |
| simpleclientInc | 6.98K | ± 105.77 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.91K | ± 308.77 | ops/s | 4.6x slower |
| simpleclientAdd | 6.58K | ± 218.28 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.39K | ± 50.58 | ops/s | 23x slower |
| openTelemetryInc | 1.39K | ± 55.11 | ops/s | 23x slower |
| openTelemetryAdd | 1.34K | ± 33.13 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.58K | ± 25.11 | ops/s | **fastest** |
| prometheusClassic | 3.01K | ± 421.46 | ops/s | 1.5x slower |
| prometheusNative | 2.27K | ± 23.55 | ops/s | 2.0x slower |
| openTelemetryClassic | 531.81 | ± 29.72 | ops/s | 8.6x slower |
| openTelemetryExponential | 400.34 | ± 14.77 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 320.09K | ± 1.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 317.58K | ± 2.14K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 300.37K | ± 1.16K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 298.36K | ± 1.30K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28972.477    ± 658.757  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1336.690     ± 33.126  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1385.220     ± 55.114  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1393.002     ± 50.583  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28606.599    ± 266.487  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31576.055     ± 58.883  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31035.833    ± 176.345  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6575.273    ± 218.279  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6983.869    ± 105.766  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6905.977    ± 308.772  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        531.814     ± 29.722  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        400.341     ± 14.773  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3005.015    ± 421.462  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2274.770     ± 23.549  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4580.658     ± 25.112  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     298356.235   ± 1297.129  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     300365.647   ± 1163.951  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     317582.191   ± 2138.808  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     320093.939   ± 1322.370  ops/s
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
