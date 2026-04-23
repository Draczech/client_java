# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-23T05:57:42Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.05K | ± 813.25 | ops/s | **fastest** |
| codahaleIncNoLabels | 30.24K | ± 1.23K | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 28.75K | ± 693.24 | ops/s | 1.1x slower |
| prometheusAdd | 27.44K | ± 1.68K | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.89K | ± 185.17 | ops/s | 4.5x slower |
| simpleclientInc | 6.85K | ± 74.87 | ops/s | 4.5x slower |
| simpleclientAdd | 6.56K | ± 177.94 | ops/s | 4.7x slower |
| openTelemetryAdd | 1.42K | ± 30.48 | ops/s | 22x slower |
| openTelemetryIncNoLabels | 1.42K | ± 91.23 | ops/s | 22x slower |
| openTelemetryInc | 1.37K | ± 156.84 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.50K | ± 83.50 | ops/s | **fastest** |
| prometheusClassic | 2.96K | ± 343.80 | ops/s | 1.5x slower |
| prometheusNative | 2.13K | ± 129.55 | ops/s | 2.1x slower |
| openTelemetryClassic | 534.33 | ± 35.59 | ops/s | 8.4x slower |
| openTelemetryExponential | 398.40 | ± 15.80 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 320.15K | ± 1.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 317.50K | ± 3.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 299.88K | ± 1.71K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 297.80K | ± 2.91K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30239.045   ± 1228.202  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1423.136     ± 30.479  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1366.663    ± 156.840  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1416.746     ± 91.234  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27436.599   ± 1680.825  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31053.585    ± 813.247  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      28754.996    ± 693.244  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6563.168    ± 177.944  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6847.286     ± 74.875  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6893.523    ± 185.169  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        534.330     ± 35.589  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        398.398     ± 15.800  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2960.926    ± 343.798  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2132.481    ± 129.550  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4496.892     ± 83.497  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297798.265   ± 2906.229  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     299880.167   ± 1712.287  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     317499.311   ± 3235.564  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     320154.399   ± 1675.717  ops/s
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
