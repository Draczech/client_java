# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-27T06:52:20Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.19K | ± 1.36K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.74K | ± 285.10 | ops/s | 1.1x slower |
| prometheusAdd | 51.55K | ± 70.40 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.34K | ± 196.50 | ops/s | 1.4x slower |
| simpleclientInc | 6.56K | ± 222.56 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 190.84 | ops/s | 10x slower |
| simpleclientAdd | 6.45K | ± 31.33 | ops/s | 10x slower |
| openTelemetryAdd | 1.42K | ± 403.89 | ops/s | 46x slower |
| openTelemetryInc | 1.34K | ± 225.00 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.31K | ± 104.11 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.00K | ± 1.61K | ops/s | **fastest** |
| simpleclient | 4.34K | ± 121.49 | ops/s | 1.2x slower |
| prometheusNative | 2.78K | ± 368.73 | ops/s | 1.8x slower |
| openTelemetryClassic | 666.10 | ± 26.16 | ops/s | 7.5x slower |
| openTelemetryExponential | 541.00 | ± 29.19 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 483.10K | ± 1.89K | ops/s | **fastest** |
| prometheusWriteToNull | 479.34K | ± 1.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 472.94K | ± 5.56K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.60K | ± 2.57K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47342.775    ± 196.503  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1422.669    ± 403.889  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1339.244    ± 224.995  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1313.884    ± 104.112  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51546.677     ± 70.403  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65191.437   ± 1355.905  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56738.573    ± 285.103  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6447.388     ± 31.334  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6563.408    ± 222.562  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6481.328    ± 190.841  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        666.097     ± 26.161  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.005     ± 29.189  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5002.321   ± 1612.104  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2777.884    ± 368.730  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4339.213    ± 121.492  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467602.547   ± 2569.887  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     472944.054   ± 5562.665  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483098.495   ± 1893.055  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     479336.918   ± 1591.322  ops/s
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
