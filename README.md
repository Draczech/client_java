# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-18T04:01:59Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.82K | ± 199.03 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.51K | ± 160.21 | ops/s | 1.2x slower |
| prometheusAdd | 50.61K | ± 1.48K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.40K | ± 634.48 | ops/s | 1.3x slower |
| simpleclientInc | 6.71K | ± 14.40 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.32K | ± 88.47 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 226.00 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.41K | ± 201.68 | ops/s | 47x slower |
| openTelemetryInc | 1.36K | ± 163.75 | ops/s | 48x slower |
| openTelemetryAdd | 1.27K | ± 38.39 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.17K | ± 1.71K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 23.73 | ops/s | 1.4x slower |
| prometheusNative | 2.95K | ± 300.06 | ops/s | 2.1x slower |
| openTelemetryClassic | 668.15 | ± 19.43 | ops/s | 9.2x slower |
| openTelemetryExponential | 572.32 | ± 27.22 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 480.40K | ± 4.11K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.89K | ± 4.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 469.28K | ± 6.93K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.69K | ± 3.24K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49402.956    ± 634.484  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1266.192     ± 38.392  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1360.326    ± 163.748  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1412.657    ± 201.682  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50606.480   ± 1483.588  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65816.215    ± 199.026  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56514.874    ± 160.213  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6185.631    ± 226.003  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6705.384     ± 14.405  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6317.106     ± 88.467  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        668.154     ± 19.435  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        572.320     ± 27.221  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6171.254   ± 1709.704  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2952.290    ± 300.064  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4404.010     ± 23.725  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464687.003   ± 3241.635  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     469284.723   ± 6932.084  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479891.361   ± 4424.419  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     480395.320   ± 4110.718  ops/s
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
