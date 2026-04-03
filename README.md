# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-03T05:34:22Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.61K | ± 35.18 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.18K | ± 69.33 | ops/s | 1.0x slower |
| prometheusAdd | 28.51K | ± 27.71 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 28.23K | ± 1.02K | ops/s | 1.1x slower |
| simpleclientInc | 6.86K | ± 102.78 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.59K | ± 270.20 | ops/s | 4.8x slower |
| simpleclientAdd | 6.42K | ± 228.17 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 1.47K | ± 261.77 | ops/s | 21x slower |
| openTelemetryInc | 1.35K | ± 91.72 | ops/s | 23x slower |
| openTelemetryAdd | 1.25K | ± 34.46 | ops/s | 25x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.49K | ± 22.83 | ops/s | **fastest** |
| prometheusClassic | 2.64K | ± 316.53 | ops/s | 1.7x slower |
| prometheusNative | 2.19K | ± 195.77 | ops/s | 2.0x slower |
| openTelemetryClassic | 552.79 | ± 12.07 | ops/s | 8.1x slower |
| openTelemetryExponential | 410.11 | ± 12.99 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 323.80K | ± 1.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 322.33K | ± 1.54K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 304.98K | ± 2.91K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 303.00K | ± 979.67 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28233.030   ± 1017.267  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1253.351     ± 34.464  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1346.586     ± 91.724  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1470.904    ± 261.769  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28508.867     ± 27.706  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31613.492     ± 35.181  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31179.936     ± 69.332  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6416.656    ± 228.168  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6862.862    ± 102.784  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6586.282    ± 270.199  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        552.792     ± 12.066  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        410.115     ± 12.986  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2639.928    ± 316.532  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2190.363    ± 195.772  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4486.747     ± 22.834  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     302997.233    ± 979.666  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     304977.982   ± 2911.334  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     322332.505   ± 1537.926  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     323802.366   ± 1211.189  ops/s
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
