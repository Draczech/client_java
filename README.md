# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-16T08:28:22Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.48K | ± 1.39K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.75K | ± 413.49 | ops/s | 1.2x slower |
| prometheusAdd | 51.33K | ± 72.36 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.46K | ± 1.52K | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 53.78 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.35K | ± 207.00 | ops/s | 10x slower |
| simpleclientAdd | 6.14K | ± 218.77 | ops/s | 11x slower |
| openTelemetryInc | 1.48K | ± 180.51 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.42K | ± 157.02 | ops/s | 46x slower |
| openTelemetryAdd | 1.26K | ± 15.33 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.27K | ± 1.34K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 86.82 | ops/s | 1.4x slower |
| prometheusNative | 2.75K | ± 253.57 | ops/s | 2.3x slower |
| openTelemetryClassic | 717.74 | ± 37.95 | ops/s | 8.7x slower |
| openTelemetryExponential | 550.32 | ± 18.31 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.17K | ± 5.43K | ops/s | **fastest** |
| prometheusWriteToByteArray | 476.25K | ± 4.99K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 472.09K | ± 6.13K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.98K | ± 5.28K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47459.807   ± 1523.636  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1263.082     ± 15.329  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1481.617    ± 180.506  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1415.552    ± 157.021  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51334.934     ± 72.357  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65482.165   ± 1387.073  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56753.830    ± 413.494  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6140.887    ± 218.773  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6664.933     ± 53.777  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6348.707    ± 206.995  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        717.739     ± 37.954  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.317     ± 18.307  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6267.035   ± 1335.174  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2754.318    ± 253.568  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4417.762     ± 86.823  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463983.545   ± 5278.270  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     472087.994   ± 6132.543  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476251.757   ± 4994.806  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489170.463   ± 5432.198  ops/s
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
