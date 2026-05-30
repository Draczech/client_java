# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-30T06:55:22Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.66K | ± 2.81K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.14K | ± 525.40 | ops/s | 1.1x slower |
| prometheusAdd | 48.43K | ± 1.00K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.42K | ± 462.73 | ops/s | 1.3x slower |
| simpleclientInc | 6.18K | ± 99.48 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.03K | ± 177.56 | ops/s | 9.7x slower |
| simpleclientAdd | 5.88K | ± 269.56 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.36K | ± 132.10 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.28K | ± 11.87 | ops/s | 46x slower |
| openTelemetryInc | 1.27K | ± 62.96 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.02K | ± 1.08K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 76.25 | ops/s | 1.4x slower |
| prometheusNative | 2.88K | ± 299.38 | ops/s | 2.1x slower |
| openTelemetryClassic | 603.50 | ± 12.49 | ops/s | 10.0x slower |
| openTelemetryExponential | 508.49 | ± 26.59 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.38K | ± 3.76K | ops/s | **fastest** |
| prometheusWriteToByteArray | 548.47K | ± 7.49K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 531.90K | ± 4.76K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.94K | ± 2.76K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44423.551    ± 462.733  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1362.618    ± 132.104  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1273.029     ± 62.964  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1279.469     ± 11.867  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48430.184   ± 1002.326  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58658.533   ± 2807.351  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52144.496    ± 525.396  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5877.219    ± 269.556  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6182.890     ± 99.484  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6029.035    ± 177.561  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        603.501     ± 12.492  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        508.490     ± 26.587  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6017.226   ± 1076.233  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2883.183    ± 299.384  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4429.754     ± 76.246  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524942.859   ± 2755.265  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     531895.365   ± 4756.641  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548471.633   ± 7490.459  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556384.617   ± 3759.121  ops/s
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
