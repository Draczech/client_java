# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-18T08:03:51Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.63K | ± 322.01 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.14K | ± 142.96 | ops/s | 1.2x slower |
| prometheusAdd | 51.45K | ± 120.04 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.17K | ± 1.93K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 159.28 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.38K | ± 182.75 | ops/s | 10x slower |
| simpleclientAdd | 6.00K | ± 102.94 | ops/s | 11x slower |
| openTelemetryInc | 1.45K | ± 203.86 | ops/s | 46x slower |
| openTelemetryAdd | 1.43K | ± 297.71 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.37K | ± 144.45 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.88K | ± 745.29 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 37.95 | ops/s | 1.1x slower |
| prometheusNative | 2.74K | ± 165.56 | ops/s | 1.8x slower |
| openTelemetryClassic | 698.96 | ± 34.85 | ops/s | 7.0x slower |
| openTelemetryExponential | 582.58 | ± 20.41 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 488.40K | ± 4.92K | ops/s | **fastest** |
| prometheusWriteToNull | 487.63K | ± 7.23K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 483.10K | ± 7.17K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.36K | ± 9.73K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49167.649   ± 1927.937  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1426.649    ± 297.707  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1451.468    ± 203.857  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1365.198    ± 144.451  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51449.615    ± 120.037  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66625.664    ± 322.011  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57144.753    ± 142.965  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5996.083    ± 102.935  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6591.213    ± 159.284  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6382.016    ± 182.755  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        698.962     ± 34.850  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        582.581     ± 20.409  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4881.035    ± 745.293  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2739.463    ± 165.556  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4465.598     ± 37.954  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478357.109   ± 9733.714  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488403.863   ± 4918.022  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483104.124   ± 7169.544  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487630.956   ± 7226.140  ops/s
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
