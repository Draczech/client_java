# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-17T05:22:45Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.09K | ± 1.94K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.29K | ± 1.32K | ops/s | 1.2x slower |
| prometheusAdd | 51.48K | ± 168.56 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.03K | ± 495.78 | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 126.14 | ops/s | 9.9x slower |
| simpleclientAdd | 6.54K | ± 27.30 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.44K | ± 7.47 | ops/s | 10x slower |
| openTelemetryAdd | 1.39K | ± 246.77 | ops/s | 48x slower |
| openTelemetryInc | 1.35K | ± 210.24 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.21K | ± 30.41 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 1.24K | ops/s | **fastest** |
| simpleclient | 4.57K | ± 44.03 | ops/s | 1.2x slower |
| prometheusNative | 2.62K | ± 92.24 | ops/s | 2.0x slower |
| openTelemetryClassic | 739.46 | ± 39.25 | ops/s | 7.2x slower |
| openTelemetryExponential | 545.09 | ± 29.09 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.43K | ± 2.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 492.80K | ± 1.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 489.54K | ± 1.40K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 489.08K | ± 3.90K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50033.489    ± 495.780  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1390.682    ± 246.766  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1352.084    ± 210.239  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1208.505     ± 30.414  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51479.883    ± 168.557  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66089.240   ± 1943.203  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56285.036   ± 1323.260  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6538.538     ± 27.301  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6687.912    ± 126.140  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6442.429      ± 7.468  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        739.461     ± 39.249  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.092     ± 29.087  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5359.436   ± 1239.340  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2622.474     ± 92.244  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4574.346     ± 44.026  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     489539.060   ± 1400.963  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489076.741   ± 3896.104  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492796.329   ± 1360.289  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495425.212   ± 2788.045  ops/s
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
