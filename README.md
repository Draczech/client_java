# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-28T05:24:11Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.57K | ± 683.87 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.18K | ± 93.82 | ops/s | 1.2x slower |
| prometheusAdd | 51.29K | ± 350.07 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.30K | ± 1.54K | ops/s | 1.4x slower |
| simpleclientInc | 6.67K | ± 51.65 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.48K | ± 196.96 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 251.24 | ops/s | 11x slower |
| openTelemetryAdd | 1.44K | ± 270.33 | ops/s | 46x slower |
| openTelemetryInc | 1.29K | ± 80.35 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.17K | ± 32.27 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.10K | ± 2.45K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 29.87 | ops/s | 1.6x slower |
| prometheusNative | 2.96K | ± 391.24 | ops/s | 2.4x slower |
| openTelemetryClassic | 733.64 | ± 17.09 | ops/s | 9.7x slower |
| openTelemetryExponential | 562.81 | ± 18.34 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.91K | ± 12.50K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.05K | ± 7.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.49K | ± 13.61K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 467.71K | ± 9.40K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49295.545   ± 1535.196  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1435.507    ± 270.327  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1292.252     ± 80.345  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1167.608     ± 32.267  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51294.779    ± 350.071  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66569.507    ± 683.867  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57175.021     ± 93.823  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6186.929    ± 251.241  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6674.886     ± 51.649  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6479.915    ± 196.959  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        733.643     ± 17.092  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.807     ± 18.337  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7101.113   ± 2446.504  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2956.649    ± 391.241  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4409.414     ± 29.873  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469491.519  ± 13611.370  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     467706.128   ± 9404.086  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486047.060   ± 7271.932  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494909.430  ± 12499.330  ops/s
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
