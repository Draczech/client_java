# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-13T05:13:16Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.02K | ± 1.43K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.08K | ± 135.07 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.80K | ± 570.36 | ops/s | 1.3x slower |
| prometheusAdd | 48.14K | ± 4.90K | ops/s | 1.4x slower |
| simpleclientInc | 6.68K | ± 14.13 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.40K | ± 101.73 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 207.38 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.51K | ± 127.14 | ops/s | 44x slower |
| openTelemetryInc | 1.47K | ± 194.62 | ops/s | 45x slower |
| openTelemetryAdd | 1.36K | ± 167.70 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.55K | ± 2.02K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 68.23 | ops/s | 1.2x slower |
| prometheusNative | 2.92K | ± 174.33 | ops/s | 1.9x slower |
| openTelemetryClassic | 679.46 | ± 27.02 | ops/s | 8.2x slower |
| openTelemetryExponential | 575.03 | ± 19.85 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 481.66K | ± 7.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 476.96K | ± 7.16K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.60K | ± 5.01K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.93K | ± 4.96K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49797.306    ± 570.356  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1355.450    ± 167.701  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1470.796    ± 194.624  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1508.631    ± 127.136  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48136.884   ± 4898.179  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66023.632   ± 1434.590  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57077.787    ± 135.067  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6315.121    ± 207.384  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6682.517     ± 14.128  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6397.737    ± 101.728  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.457     ± 27.023  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.027     ± 19.851  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5546.736   ± 2018.521  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2924.719    ± 174.328  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4448.328     ± 68.226  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469932.010   ± 4960.446  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471598.162   ± 5005.249  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476957.017   ± 7164.843  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481657.464   ± 7173.739  ops/s
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
