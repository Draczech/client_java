# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-03T06:36:02Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.31K | ± 393.29 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.78K | ± 70.74 | ops/s | 1.1x slower |
| prometheusAdd | 48.10K | ± 341.13 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.39K | ± 357.04 | ops/s | 1.3x slower |
| simpleclientInc | 6.28K | ± 60.19 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.13K | ± 184.08 | ops/s | 9.7x slower |
| simpleclientAdd | 5.91K | ± 125.86 | ops/s | 10x slower |
| openTelemetryAdd | 1.30K | ± 48.09 | ops/s | 46x slower |
| openTelemetryInc | 1.30K | ± 18.02 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.24K | ± 86.41 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.84K | ± 1.79K | ops/s | **fastest** |
| simpleclient | 4.36K | ± 60.28 | ops/s | 1.3x slower |
| prometheusNative | 3.18K | ± 53.93 | ops/s | 1.8x slower |
| openTelemetryClassic | 612.85 | ± 11.50 | ops/s | 9.5x slower |
| openTelemetryExponential | 516.09 | ± 13.56 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 558.53K | ± 4.40K | ops/s | **fastest** |
| openMetricsWriteToNull | 539.92K | ± 4.67K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 529.92K | ± 16.14K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 524.80K | ± 7.04K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44388.531    ± 357.036  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1302.714     ± 48.089  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1298.716     ± 18.019  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1239.890     ± 86.411  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48096.164    ± 341.130  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59309.005    ± 393.290  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51778.196     ± 70.736  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5911.285    ± 125.860  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6275.528     ± 60.188  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6132.885    ± 184.077  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        612.846     ± 11.495  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        516.086     ± 13.565  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5837.303   ± 1788.706  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3175.914     ± 53.929  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4360.112     ± 60.279  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524804.088   ± 7044.025  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     539916.834   ± 4673.572  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     529924.512  ± 16136.823  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     558534.744   ± 4402.659  ops/s
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
