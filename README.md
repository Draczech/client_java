# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-24T06:01:22Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.36K | ± 3.18K | ops/s | **fastest** |
| prometheusNoLabelsInc | 59.62K | ± 517.16 | ops/s | 1.1x slower |
| prometheusAdd | 53.52K | ± 506.79 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.31K | ± 542.20 | ops/s | 1.3x slower |
| simpleclientInc | 6.96K | ± 64.57 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.77K | ± 182.51 | ops/s | 9.8x slower |
| simpleclientAdd | 6.47K | ± 239.79 | ops/s | 10x slower |
| openTelemetryInc | 1.49K | ± 283.28 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.40K | ± 148.51 | ops/s | 47x slower |
| openTelemetryAdd | 1.34K | ± 28.18 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.73K | ± 2.42K | ops/s | **fastest** |
| simpleclient | 4.59K | ± 87.12 | ops/s | 1.5x slower |
| prometheusNative | 3.39K | ± 98.40 | ops/s | 2.0x slower |
| openTelemetryClassic | 714.20 | ± 28.53 | ops/s | 9.4x slower |
| openTelemetryExponential | 568.22 | ± 27.30 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 525.67K | ± 2.05K | ops/s | **fastest** |
| prometheusWriteToByteArray | 513.06K | ± 1.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 504.29K | ± 3.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 498.35K | ± 8.46K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49306.378    ± 542.198  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1337.565     ± 28.175  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1494.267    ± 283.276  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1399.337    ± 148.513  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      53517.724    ± 506.790  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66362.803   ± 3184.736  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      59616.147    ± 517.162  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6468.826    ± 239.791  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6963.071     ± 64.570  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6765.794    ± 182.510  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        714.200     ± 28.533  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        568.216     ± 27.301  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6726.761   ± 2420.135  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3390.152     ± 98.403  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4589.412     ± 87.116  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     498345.080   ± 8457.067  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     504287.624   ± 3100.957  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     513058.532   ± 1216.205  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     525672.034   ± 2050.007  ops/s
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
