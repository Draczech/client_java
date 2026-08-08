# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-08T04:31:05Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.06K | ± 995.26 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.22K | ± 604.21 | ops/s | 1.2x slower |
| prometheusAdd | 48.28K | ± 379.21 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.60K | ± 736.14 | ops/s | 1.3x slower |
| simpleclientInc | 6.19K | ± 123.53 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.07K | ± 306.79 | ops/s | 9.9x slower |
| simpleclientAdd | 5.92K | ± 103.39 | ops/s | 10x slower |
| openTelemetryAdd | 1.50K | ± 142.67 | ops/s | 40x slower |
| openTelemetryInc | 1.41K | ± 68.04 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.36K | ± 50.04 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.93K | ± 571.69 | ops/s | **fastest** |
| simpleclient | 4.51K | ± 58.00 | ops/s | 1.1x slower |
| prometheusNative | 3.01K | ± 257.84 | ops/s | 1.6x slower |
| openTelemetryClassic | 623.95 | ± 35.27 | ops/s | 7.9x slower |
| openTelemetryExponential | 552.47 | ± 29.52 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 558.83K | ± 7.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 550.47K | ± 1.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 542.76K | ± 3.25K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.33K | ± 7.08K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44601.385    ± 736.142  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1498.863    ± 142.674  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1411.735     ± 68.035  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1355.758     ± 50.043  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48284.457    ± 379.209  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60060.358    ± 995.261  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51217.081    ± 604.208  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5915.778    ± 103.394  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6192.260    ± 123.532  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6073.430    ± 306.789  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        623.952     ± 35.271  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        552.471     ± 29.523  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4928.235    ± 571.686  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3008.368    ± 257.845  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4513.616     ± 58.004  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524330.019   ± 7077.397  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     542761.071   ± 3248.973  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     550472.602   ± 1626.610  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     558833.468   ± 7171.178  ops/s
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
