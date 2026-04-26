# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-26T06:05:55Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.50K | ± 94.86 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.13K | ± 241.47 | ops/s | 1.2x slower |
| prometheusAdd | 51.10K | ± 445.88 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.26K | ± 871.89 | ops/s | 1.4x slower |
| simpleclientInc | 6.58K | ± 163.49 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.41K | ± 167.80 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 236.59 | ops/s | 11x slower |
| openTelemetryAdd | 1.26K | ± 69.46 | ops/s | 53x slower |
| openTelemetryInc | 1.25K | ± 72.49 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.19K | ± 29.79 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.35K | ± 1.26K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 91.38 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 165.30 | ops/s | 1.8x slower |
| openTelemetryClassic | 669.60 | ± 37.02 | ops/s | 8.0x slower |
| openTelemetryExponential | 572.74 | ± 26.95 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.32K | ± 4.00K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.11K | ± 1.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.89K | ± 3.00K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.29K | ± 4.31K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48256.763    ± 871.888  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1257.652     ± 69.455  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1249.749     ± 72.494  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1191.843     ± 29.790  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51097.534    ± 445.880  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66498.645     ± 94.857  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57129.692    ± 241.471  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6187.117    ± 236.591  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6577.019    ± 163.489  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6412.194    ± 167.800  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        669.596     ± 37.023  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        572.741     ± 26.952  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5350.002   ± 1263.118  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3049.218    ± 165.301  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4389.228     ± 91.375  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478293.982   ± 4314.866  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483890.737   ± 3002.333  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487109.799   ± 1802.819  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489317.802   ± 4001.515  ops/s
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
