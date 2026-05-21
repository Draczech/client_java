# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-21T07:15:46Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.11K | ± 1.21K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.13K | ± 373.07 | ops/s | 1.2x slower |
| prometheusAdd | 48.67K | ± 938.46 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.19K | ± 335.72 | ops/s | 1.4x slower |
| simpleclientInc | 6.19K | ± 115.80 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.01K | ± 151.77 | ops/s | 10.0x slower |
| simpleclientAdd | 5.65K | ± 160.01 | ops/s | 11x slower |
| openTelemetryAdd | 1.49K | ± 116.14 | ops/s | 40x slower |
| openTelemetryInc | 1.40K | ± 34.47 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.37K | ± 29.11 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.35K | ± 83.48 | ops/s | **fastest** |
| prometheusClassic | 4.33K | ± 547.41 | ops/s | 1.0x slower |
| prometheusNative | 3.13K | ± 94.46 | ops/s | 1.4x slower |
| openTelemetryClassic | 626.65 | ± 22.18 | ops/s | 6.9x slower |
| openTelemetryExponential | 511.71 | ± 2.85 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 541.31K | ± 4.69K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.56K | ± 2.48K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 521.36K | ± 4.58K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 505.50K | ± 8.44K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44191.023    ± 335.722  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1488.597    ± 116.145  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1395.172     ± 34.473  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1366.142     ± 29.106  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48666.723    ± 938.458  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60112.858   ± 1213.867  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52125.865    ± 373.070  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5648.465    ± 160.013  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6190.318    ± 115.798  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6013.260    ± 151.766  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        626.650     ± 22.185  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        511.709      ± 2.847  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4334.040    ± 547.410  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3132.995     ± 94.464  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4348.145     ± 83.480  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505495.997   ± 8441.401  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     521355.562   ± 4577.235  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524557.811   ± 2478.017  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     541311.134   ± 4690.694  ops/s
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
