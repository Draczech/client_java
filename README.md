# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-25T06:09:34Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.26K | ± 322.43 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 420.11 | ops/s | 1.2x slower |
| prometheusAdd | 50.18K | ± 1.36K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.96K | ± 1.38K | ops/s | 1.4x slower |
| simpleclientInc | 6.41K | ± 139.22 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 187.11 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.23K | ± 31.68 | ops/s | 11x slower |
| openTelemetryAdd | 1.47K | ± 217.24 | ops/s | 45x slower |
| openTelemetryInc | 1.37K | ± 131.68 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.26K | ± 45.16 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.59K | ± 1.32K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 54.23 | ops/s | 1.3x slower |
| prometheusNative | 3.14K | ± 143.45 | ops/s | 1.8x slower |
| openTelemetryClassic | 701.98 | ± 43.89 | ops/s | 8.0x slower |
| openTelemetryExponential | 572.54 | ± 23.04 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.13K | ± 5.13K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.49K | ± 3.49K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.93K | ± 2.63K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.53K | ± 7.04K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47955.856   ± 1383.999  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1471.616    ± 217.238  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1371.568    ± 131.682  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1261.558     ± 45.163  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50178.784   ± 1360.642  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66260.072    ± 322.431  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56834.254    ± 420.107  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6333.672    ± 187.112  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6412.403    ± 139.223  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6229.725     ± 31.677  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        701.985     ± 43.891  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        572.538     ± 23.037  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5585.744   ± 1315.138  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3138.021    ± 143.453  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4420.774     ± 54.230  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471534.078   ± 7039.227  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480930.140   ± 2625.423  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484485.885   ± 3488.784  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491129.132   ± 5134.254  ops/s
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
