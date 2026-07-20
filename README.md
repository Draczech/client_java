# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-20T06:42:27Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.38K | ± 500.03 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.11K | ± 108.64 | ops/s | 1.2x slower |
| prometheusAdd | 51.39K | ± 154.21 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.39K | ± 720.83 | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 198.88 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 199.64 | ops/s | 10x slower |
| simpleclientAdd | 6.05K | ± 43.00 | ops/s | 11x slower |
| openTelemetryAdd | 1.30K | ± 72.34 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.21K | ± 27.21 | ops/s | 55x slower |
| openTelemetryInc | 1.21K | ± 11.11 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.81K | ± 690.42 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 54.11 | ops/s | 1.1x slower |
| prometheusNative | 2.78K | ± 263.12 | ops/s | 1.7x slower |
| openTelemetryClassic | 690.36 | ± 12.94 | ops/s | 7.0x slower |
| openTelemetryExponential | 568.66 | ± 37.12 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 481.97K | ± 4.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 471.86K | ± 4.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 467.36K | ± 4.80K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 456.44K | ± 4.72K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49393.587    ± 720.832  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1299.344     ± 72.336  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1212.286     ± 11.109  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1213.235     ± 27.207  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51393.861    ± 154.209  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66377.232    ± 500.030  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57112.332    ± 108.637  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6046.222     ± 42.996  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6533.168    ± 198.883  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6343.020    ± 199.640  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        690.356     ± 12.939  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        568.661     ± 37.121  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4813.478    ± 690.416  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2783.006    ± 263.120  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4440.136     ± 54.109  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     456442.115   ± 4719.989  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     467364.950   ± 4795.187  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     471855.697   ± 4557.990  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481968.012   ± 4938.486  ops/s
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
