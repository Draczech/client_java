# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-29T07:18:34Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 30.72K | ± 1.10K | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.52K | ± 961.11 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.04K | ± 1.33K | ops/s | 1.1x slower |
| prometheusAdd | 27.96K | ± 1.04K | ops/s | 1.1x slower |
| simpleclientInc | 6.87K | ± 90.44 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.80K | ± 154.15 | ops/s | 4.5x slower |
| simpleclientAdd | 6.39K | ± 28.51 | ops/s | 4.8x slower |
| openTelemetryInc | 1.51K | ± 89.33 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 1.48K | ± 143.99 | ops/s | 21x slower |
| openTelemetryAdd | 1.40K | ± 36.06 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.48K | ± 80.95 | ops/s | **fastest** |
| prometheusClassic | 3.62K | ± 1.11K | ops/s | 1.2x slower |
| prometheusNative | 2.30K | ± 221.81 | ops/s | 2.0x slower |
| openTelemetryClassic | 502.75 | ± 19.23 | ops/s | 8.9x slower |
| openTelemetryExponential | 388.30 | ± 12.82 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 324.70K | ± 1.38K | ops/s | **fastest** |
| prometheusWriteToByteArray | 320.82K | ± 1.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 304.04K | ± 2.90K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 302.25K | ± 1.37K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29044.203   ± 1332.745  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1401.107     ± 36.062  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1513.045     ± 89.331  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1476.851    ± 143.986  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27956.315   ± 1040.255  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30717.392   ± 1101.627  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30523.030    ± 961.105  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6391.989     ± 28.514  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6873.170     ± 90.439  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6800.119    ± 154.155  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        502.748     ± 19.229  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        388.298     ± 12.816  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3618.327   ± 1111.198  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2295.364    ± 221.809  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4481.094     ± 80.953  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     302247.709   ± 1370.206  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     304044.177   ± 2902.111  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     320823.295   ± 1424.535  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     324701.814   ± 1376.691  ops/s
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
