# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-07T05:33:05Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.07K | ± 1.57K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.98K | ± 593.68 | ops/s | 1.1x slower |
| prometheusAdd | 51.12K | ± 688.18 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.55K | ± 616.77 | ops/s | 1.3x slower |
| simpleclientInc | 6.57K | ± 155.87 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.52K | ± 128.16 | ops/s | 9.8x slower |
| simpleclientAdd | 6.13K | ± 316.07 | ops/s | 10x slower |
| openTelemetryAdd | 1.78K | ± 118.97 | ops/s | 36x slower |
| openTelemetryInc | 1.57K | ± 74.58 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.40K | ± 200.52 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.19K | ± 1.96K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 61.83 | ops/s | 1.4x slower |
| prometheusNative | 2.76K | ± 349.60 | ops/s | 2.2x slower |
| openTelemetryClassic | 680.98 | ± 26.54 | ops/s | 9.1x slower |
| openTelemetryExponential | 562.98 | ± 47.03 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 490.00K | ± 2.80K | ops/s | **fastest** |
| openMetricsWriteToNull | 482.79K | ± 3.12K | ops/s | 1.0x slower |
| prometheusWriteToNull | 482.47K | ± 12.19K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.26K | ± 6.05K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50548.157    ± 616.769  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1783.220    ± 118.965  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1569.836     ± 74.585  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1401.933    ± 200.516  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51122.152    ± 688.184  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64069.502   ± 1568.468  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56980.066    ± 593.680  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6130.348    ± 316.066  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6565.012    ± 155.875  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6524.002    ± 128.160  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        680.983     ± 26.545  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.983     ± 47.033  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6187.878   ± 1955.636  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2756.462    ± 349.605  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4446.869     ± 61.826  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474256.564   ± 6053.459  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482788.607   ± 3118.640  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490003.751   ± 2803.821  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482468.336  ± 12194.726  ops/s
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
