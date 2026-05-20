# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-20T07:12:22Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.53K | ± 1.56K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.82K | ± 291.47 | ops/s | 1.1x slower |
| prometheusAdd | 51.30K | ± 313.17 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.24K | ± 146.01 | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 61.39 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.29K | ± 322.07 | ops/s | 10x slower |
| simpleclientAdd | 6.26K | ± 186.89 | ops/s | 10x slower |
| openTelemetryAdd | 1.50K | ± 246.36 | ops/s | 43x slower |
| openTelemetryInc | 1.28K | ± 26.96 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.24K | ± 58.78 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.79K | ± 522.25 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 48.72 | ops/s | 1.1x slower |
| prometheusNative | 3.18K | ± 46.91 | ops/s | 1.5x slower |
| openTelemetryClassic | 720.32 | ± 15.79 | ops/s | 6.7x slower |
| openTelemetryExponential | 596.45 | ± 21.15 | ops/s | 8.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.93K | ± 8.38K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.58K | ± 3.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 469.37K | ± 6.92K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 465.04K | ± 6.75K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50237.240    ± 146.008  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1500.534    ± 246.355  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1281.219     ± 26.957  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1235.158     ± 58.775  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51299.602    ± 313.168  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64534.262   ± 1558.316  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56821.726    ± 291.474  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6261.721    ± 186.893  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6661.246     ± 61.392  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6294.958    ± 322.075  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        720.317     ± 15.785  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        596.446     ± 21.147  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4794.648    ± 522.247  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3184.674     ± 46.909  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4481.897     ± 48.725  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     465040.450   ± 6752.738  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     469370.648   ± 6915.194  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479583.147   ± 3255.666  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488927.098   ± 8384.791  ops/s
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
