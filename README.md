# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-02T06:06:37Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.82K | ± 755.53 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.82K | ± 338.00 | ops/s | 1.2x slower |
| prometheusAdd | 51.16K | ± 71.99 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.14K | ± 1.65K | ops/s | 1.4x slower |
| simpleclientInc | 6.57K | ± 149.20 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.47K | ± 217.19 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 233.83 | ops/s | 11x slower |
| openTelemetryAdd | 1.39K | ± 237.45 | ops/s | 48x slower |
| openTelemetryInc | 1.28K | ± 21.85 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.21K | ± 29.78 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.28K | ± 1.50K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 75.32 | ops/s | 1.4x slower |
| prometheusNative | 2.86K | ± 328.71 | ops/s | 2.2x slower |
| openTelemetryClassic | 725.00 | ± 23.03 | ops/s | 8.7x slower |
| openTelemetryExponential | 544.84 | ± 26.02 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.11K | ± 3.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.56K | ± 2.97K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.54K | ± 1.42K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.09K | ± 1.78K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48142.114   ± 1651.425  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1391.937    ± 237.446  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1276.699     ± 21.850  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1210.018     ± 29.778  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51162.556     ± 71.993  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66817.764    ± 755.532  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56824.630    ± 338.002  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6326.155    ± 233.826  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6565.033    ± 149.205  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6471.279    ± 217.185  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        725.003     ± 23.034  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.844     ± 26.021  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6276.505   ± 1499.095  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2855.048    ± 328.708  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4424.136     ± 75.315  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477091.442   ± 1778.376  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485544.203   ± 1423.752  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489555.123   ± 2973.025  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491106.724   ± 3172.652  ops/s
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
