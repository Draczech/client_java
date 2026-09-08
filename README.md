# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-08T07:54:30Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.18K | ± 271.96 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.38K | ± 1.09K | ops/s | 1.2x slower |
| prometheusAdd | 51.00K | ± 619.96 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.83K | ± 493.04 | ops/s | 1.3x slower |
| simpleclientInc | 6.60K | ± 69.47 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.49K | ± 195.06 | ops/s | 10x slower |
| simpleclientAdd | 6.44K | ± 36.45 | ops/s | 10x slower |
| openTelemetryAdd | 1.48K | ± 318.58 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.45K | ± 169.58 | ops/s | 46x slower |
| openTelemetryInc | 1.37K | ± 137.99 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.73K | ± 1.25K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 14.06 | ops/s | 1.3x slower |
| prometheusNative | 3.00K | ± 244.71 | ops/s | 1.9x slower |
| openTelemetryClassic | 668.14 | ± 28.68 | ops/s | 8.6x slower |
| openTelemetryExponential | 537.69 | ± 20.77 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 483.89K | ± 3.07K | ops/s | **fastest** |
| prometheusWriteToByteArray | 475.08K | ± 8.54K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.99K | ± 1.25K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 466.50K | ± 3.57K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49831.910    ± 493.039  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1483.867    ± 318.582  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1367.519    ± 137.994  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1451.620    ± 169.580  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50997.551    ± 619.963  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66180.543    ± 271.957  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56380.746   ± 1088.512  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6437.259     ± 36.450  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6604.354     ± 69.470  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6491.979    ± 195.063  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        668.136     ± 28.677  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        537.694     ± 20.768  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5728.315   ± 1245.239  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3001.836    ± 244.710  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4393.115     ± 14.064  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467986.923   ± 1251.008  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     466503.083   ± 3572.824  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     475079.922   ± 8536.319  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     483886.419   ± 3071.867  ops/s
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
