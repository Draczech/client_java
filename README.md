# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-05T07:27:03Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.57K | ± 26.70 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.24K | ± 192.84 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.57K | ± 305.47 | ops/s | 1.1x slower |
| prometheusAdd | 27.89K | ± 915.71 | ops/s | 1.1x slower |
| simpleclientInc | 6.90K | ± 102.30 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.82K | ± 143.09 | ops/s | 4.6x slower |
| simpleclientAdd | 6.49K | ± 215.46 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 1.52K | ± 44.47 | ops/s | 21x slower |
| openTelemetryInc | 1.41K | ± 39.49 | ops/s | 22x slower |
| openTelemetryAdd | 1.33K | ± 98.89 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.54K | ± 39.85 | ops/s | **fastest** |
| prometheusClassic | 3.20K | ± 613.48 | ops/s | 1.4x slower |
| prometheusNative | 2.27K | ± 162.03 | ops/s | 2.0x slower |
| openTelemetryClassic | 531.08 | ± 12.62 | ops/s | 8.6x slower |
| openTelemetryExponential | 404.79 | ± 18.55 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 317.09K | ± 1.46K | ops/s | **fastest** |
| prometheusWriteToByteArray | 315.78K | ± 1.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 299.68K | ± 720.77 | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 297.38K | ± 1.31K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28569.099    ± 305.474  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1330.527     ± 98.892  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1411.861     ± 39.489  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1519.321     ± 44.468  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27890.771    ± 915.711  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31570.319     ± 26.699  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31237.179    ± 192.838  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6492.078    ± 215.464  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6899.969    ± 102.297  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6821.312    ± 143.094  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        531.080     ± 12.619  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        404.795     ± 18.550  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3199.030    ± 613.485  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2271.208    ± 162.035  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4544.067     ± 39.849  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297381.755   ± 1310.535  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     299675.131    ± 720.770  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     315777.684   ± 1875.596  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     317094.298   ± 1463.217  ops/s
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
