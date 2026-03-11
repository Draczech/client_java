# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-11T05:15:14Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.51K | ± 411.31 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.69K | ± 307.79 | ops/s | 1.2x slower |
| prometheusAdd | 50.46K | ± 1.93K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.42K | ± 704.63 | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 150.37 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.58K | ± 219.46 | ops/s | 10x slower |
| simpleclientAdd | 6.38K | ± 225.70 | ops/s | 10x slower |
| openTelemetryInc | 1.45K | ± 281.21 | ops/s | 46x slower |
| openTelemetryAdd | 1.36K | ± 320.24 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.27K | ± 101.60 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.00K | ± 1.05K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 46.83 | ops/s | 1.3x slower |
| prometheusNative | 2.94K | ± 257.58 | ops/s | 2.0x slower |
| openTelemetryClassic | 660.82 | ± 16.01 | ops/s | 9.1x slower |
| openTelemetryExponential | 527.63 | ± 16.31 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.17K | ± 3.40K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.41K | ± 4.74K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 470.70K | ± 3.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 458.05K | ± 4.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49424.858    ± 704.633  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1364.044    ± 320.244  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1447.049    ± 281.207  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1266.657    ± 101.598  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50458.158   ± 1926.746  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66511.980    ± 411.315  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56689.991    ± 307.792  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6376.993    ± 225.704  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6689.034    ± 150.374  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6580.686    ± 219.459  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        660.817     ± 16.011  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        527.626     ± 16.307  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6004.509   ± 1052.125  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2941.283    ± 257.581  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4503.385     ± 46.829  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     458054.429   ± 4288.307  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470703.308   ± 3613.203  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479406.177   ± 4736.986  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484165.572   ± 3400.524  ops/s
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
