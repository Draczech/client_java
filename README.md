# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-05T05:43:19Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.56K | ± 1.59K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.24K | ± 1.02K | ops/s | 1.2x slower |
| prometheusAdd | 51.37K | ± 343.07 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.44K | ± 1.31K | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 16.10 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.32K | ± 234.37 | ops/s | 10x slower |
| simpleclientAdd | 6.22K | ± 367.78 | ops/s | 11x slower |
| openTelemetryAdd | 1.43K | ± 280.40 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.32K | ± 178.23 | ops/s | 50x slower |
| openTelemetryInc | 1.29K | ± 19.46 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.62K | ± 798.01 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 54.30 | ops/s | 1.0x slower |
| prometheusNative | 3.00K | ± 317.07 | ops/s | 1.5x slower |
| openTelemetryClassic | 661.90 | ± 9.98 | ops/s | 7.0x slower |
| openTelemetryExponential | 548.93 | ± 9.91 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.52K | ± 1.62K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.43K | ± 4.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.33K | ± 3.08K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.99K | ± 3.50K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49435.642   ± 1305.527  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1427.892    ± 280.404  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1288.788     ± 19.464  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1320.307    ± 178.227  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51373.056    ± 343.066  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65560.488   ± 1594.733  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56241.503   ± 1019.865  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6215.444    ± 367.775  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6696.677     ± 16.103  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6321.200    ± 234.367  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        661.899      ± 9.981  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.926      ± 9.914  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4616.753    ± 798.012  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3003.143    ± 317.070  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4441.425     ± 54.299  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476989.998   ± 3504.475  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485333.716   ± 3077.757  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489429.099   ± 4904.470  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493520.073   ± 1617.667  ops/s
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
