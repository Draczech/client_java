# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-16T06:33:14Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.81K | ± 2.45K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.17K | ± 857.28 | ops/s | 1.1x slower |
| prometheusAdd | 48.10K | ± 372.42 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.23K | ± 550.10 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.28K | ± 23.71 | ops/s | 9.4x slower |
| simpleclientInc | 6.18K | ± 169.40 | ops/s | 9.5x slower |
| simpleclientAdd | 6.01K | ± 167.66 | ops/s | 9.8x slower |
| openTelemetryIncNoLabels | 1.38K | ± 161.68 | ops/s | 42x slower |
| openTelemetryAdd | 1.34K | ± 36.24 | ops/s | 44x slower |
| openTelemetryInc | 1.30K | ± 47.22 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.40K | ± 590.36 | ops/s | **fastest** |
| simpleclient | 4.16K | ± 71.84 | ops/s | 1.1x slower |
| prometheusNative | 3.10K | ± 136.53 | ops/s | 1.4x slower |
| openTelemetryClassic | 616.92 | ± 13.25 | ops/s | 7.1x slower |
| openTelemetryExponential | 520.12 | ± 20.67 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.29K | ± 2.28K | ops/s | **fastest** |
| prometheusWriteToByteArray | 550.06K | ± 1.74K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.42K | ± 8.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 526.61K | ± 4.82K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44227.203    ± 550.098  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1343.319     ± 36.243  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1302.659     ± 47.216  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1383.907    ± 161.678  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48099.902    ± 372.416  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58807.425   ± 2453.249  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52170.566    ± 857.277  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6007.497    ± 167.658  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6180.740    ± 169.397  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6280.895     ± 23.708  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        616.920     ± 13.245  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        520.117     ± 20.666  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4402.574    ± 590.365  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3095.902    ± 136.531  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4161.413     ± 71.839  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     526612.744   ± 4820.869  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534417.724   ± 8935.058  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     550064.928   ± 1743.395  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555292.414   ± 2282.043  ops/s
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
