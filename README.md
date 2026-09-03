# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-03T07:51:48Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.78K | ± 2.81K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.74K | ± 759.72 | ops/s | 1.1x slower |
| prometheusAdd | 48.45K | ± 257.33 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.72K | ± 1.76K | ops/s | 1.4x slower |
| simpleclientInc | 6.15K | ± 261.41 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.09K | ± 268.87 | ops/s | 9.6x slower |
| simpleclientAdd | 5.89K | ± 275.06 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.48K | ± 137.63 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.44K | ± 56.42 | ops/s | 41x slower |
| openTelemetryInc | 1.33K | ± 19.37 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.79K | ± 1.44K | ops/s | **fastest** |
| simpleclient | 4.24K | ± 29.15 | ops/s | 1.8x slower |
| prometheusNative | 2.73K | ± 112.37 | ops/s | 2.9x slower |
| openTelemetryClassic | 586.63 | ± 19.18 | ops/s | 13x slower |
| openTelemetryExponential | 507.07 | ± 8.89 | ops/s | 15x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 537.75K | ± 5.31K | ops/s | **fastest** |
| prometheusWriteToByteArray | 529.50K | ± 4.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 518.60K | ± 9.34K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 511.26K | ± 2.12K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42724.846   ± 1764.644  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1480.435    ± 137.634  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1331.642     ± 19.368  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1435.270     ± 56.423  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48446.382    ± 257.331  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58777.414   ± 2813.059  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51743.121    ± 759.723  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5893.518    ± 275.055  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6146.419    ± 261.411  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6091.376    ± 268.872  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        586.634     ± 19.181  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        507.065      ± 8.885  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7787.129   ± 1444.903  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2726.965    ± 112.373  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4235.302     ± 29.146  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     511261.871   ± 2123.632  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     518603.326   ± 9336.269  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     529496.459   ± 4679.298  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     537746.407   ± 5310.858  ops/s
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
