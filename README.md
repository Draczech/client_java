# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-19T08:10:13Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.63K | ± 1.63K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.18K | ± 2.72K | ops/s | 1.2x slower |
| prometheusAdd | 48.40K | ± 99.53 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 37.39K | ± 10.29K | ops/s | 1.6x slower |
| simpleclientInc | 6.22K | ± 124.89 | ops/s | 9.6x slower |
| simpleclientAdd | 6.04K | ± 173.31 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.85K | ± 86.64 | ops/s | 10x slower |
| openTelemetryInc | 1.46K | ± 171.67 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.43K | ± 157.43 | ops/s | 42x slower |
| openTelemetryAdd | 1.41K | ± 46.36 | ops/s | 42x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.85K | ± 1.33K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 32.74 | ops/s | 1.3x slower |
| prometheusNative | 3.14K | ± 308.22 | ops/s | 1.9x slower |
| openTelemetryClassic | 633.94 | ± 40.22 | ops/s | 9.2x slower |
| openTelemetryExponential | 523.87 | ± 21.91 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 536.16K | ± 3.44K | ops/s | **fastest** |
| prometheusWriteToByteArray | 532.14K | ± 4.50K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 515.11K | ± 2.96K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 508.74K | ± 3.31K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      37393.665  ± 10288.116  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1406.058     ± 46.359  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1456.046    ± 171.670  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1434.269    ± 157.429  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48404.703     ± 99.529  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59633.051   ± 1632.609  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50176.427   ± 2717.491  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6041.396    ± 173.314  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6221.297    ± 124.886  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5851.229     ± 86.645  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        633.938     ± 40.221  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        523.873     ± 21.911  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5851.928   ± 1331.971  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3136.019    ± 308.225  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4541.822     ± 32.737  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508740.302   ± 3309.207  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     515105.794   ± 2960.042  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     532143.550   ± 4499.865  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     536160.764   ± 3438.215  ops/s
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
