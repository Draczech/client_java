# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-05T07:08:23Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.59K | ± 22.18 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.11K | ± 44.27 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.72K | ± 1.55K | ops/s | 1.1x slower |
| prometheusAdd | 28.55K | ± 147.98 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 6.74K | ± 191.88 | ops/s | 4.7x slower |
| simpleclientInc | 6.72K | ± 103.68 | ops/s | 4.7x slower |
| simpleclientAdd | 6.50K | ± 215.27 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 1.44K | ± 45.09 | ops/s | 22x slower |
| openTelemetryAdd | 1.27K | ± 52.49 | ops/s | 25x slower |
| openTelemetryInc | 1.25K | ± 65.61 | ops/s | 25x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.51K | ± 66.48 | ops/s | **fastest** |
| prometheusClassic | 3.27K | ± 191.02 | ops/s | 1.4x slower |
| prometheusNative | 2.08K | ± 177.47 | ops/s | 2.2x slower |
| openTelemetryClassic | 501.16 | ± 27.54 | ops/s | 9.0x slower |
| openTelemetryExponential | 415.36 | ± 18.28 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 319.88K | ± 959.47 | ops/s | **fastest** |
| prometheusWriteToByteArray | 315.39K | ± 1.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 301.19K | ± 1.04K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 297.28K | ± 1.98K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29716.306   ± 1553.102  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1266.132     ± 52.491  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1248.950     ± 65.610  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1435.778     ± 45.087  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28548.860    ± 147.985  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31587.514     ± 22.176  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31106.069     ± 44.269  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6504.935    ± 215.271  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6724.515    ± 103.682  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6744.914    ± 191.881  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        501.158     ± 27.544  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        415.360     ± 18.282  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3270.302    ± 191.025  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2075.795    ± 177.472  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4512.165     ± 66.480  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297275.081   ± 1977.500  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     301193.296   ± 1042.790  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     315392.761   ± 1268.463  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     319877.211    ± 959.466  ops/s
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
