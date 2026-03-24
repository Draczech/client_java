# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-24T05:23:05Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 30.62K | ± 1.16K | ops/s | **fastest** |
| prometheusInc | 30.30K | ± 2.00K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.93K | ± 1.15K | ops/s | 1.1x slower |
| prometheusAdd | 28.59K | ± 81.33 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.93K | ± 178.55 | ops/s | 4.4x slower |
| simpleclientInc | 6.89K | ± 97.32 | ops/s | 4.4x slower |
| simpleclientAdd | 6.88K | ± 37.18 | ops/s | 4.4x slower |
| openTelemetryIncNoLabels | 1.32K | ± 44.67 | ops/s | 23x slower |
| openTelemetryAdd | 1.31K | ± 77.92 | ops/s | 23x slower |
| openTelemetryInc | 1.30K | ± 12.85 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.58K | ± 34.35 | ops/s | **fastest** |
| prometheusClassic | 3.20K | ± 472.19 | ops/s | 1.4x slower |
| prometheusNative | 2.24K | ± 428.44 | ops/s | 2.0x slower |
| openTelemetryClassic | 483.72 | ± 28.20 | ops/s | 9.5x slower |
| openTelemetryExponential | 423.95 | ± 37.95 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 315.00K | ± 5.98K | ops/s | **fastest** |
| prometheusWriteToNull | 311.16K | ± 7.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 299.18K | ± 3.73K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 297.21K | ± 1.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28933.219   ± 1154.833  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1305.664     ± 77.923  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1297.019     ± 12.851  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1316.864     ± 44.675  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28591.638     ± 81.331  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30304.389   ± 2001.747  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30615.254   ± 1155.133  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6880.035     ± 37.176  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6885.979     ± 97.319  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6927.400    ± 178.554  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        483.720     ± 28.195  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        423.947     ± 37.951  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3203.194    ± 472.191  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2243.396    ± 428.439  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4580.540     ± 34.351  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297207.997   ± 1293.926  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     299175.180   ± 3734.264  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     315001.048   ± 5979.130  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     311164.449   ± 7300.182  ops/s
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
