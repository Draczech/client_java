# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-17T06:54:58Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.95K | ± 75.00 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.42K | ± 639.78 | ops/s | 1.2x slower |
| prometheusAdd | 47.87K | ± 49.19 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.20K | ± 765.68 | ops/s | 1.4x slower |
| simpleclientInc | 6.20K | ± 96.53 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.17K | ± 161.25 | ops/s | 9.7x slower |
| simpleclientAdd | 5.59K | ± 181.70 | ops/s | 11x slower |
| openTelemetryAdd | 1.42K | ± 108.04 | ops/s | 42x slower |
| openTelemetryInc | 1.32K | ± 73.44 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.30K | ± 7.27 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.72K | ± 1.53K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 60.25 | ops/s | 1.3x slower |
| prometheusNative | 2.95K | ± 284.58 | ops/s | 1.9x slower |
| openTelemetryClassic | 611.43 | ± 5.89 | ops/s | 9.4x slower |
| openTelemetryExponential | 534.98 | ± 20.93 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 553.43K | ± 3.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 549.08K | ± 3.95K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.12K | ± 4.66K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 521.84K | ± 4.96K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44195.959    ± 765.680  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1416.135    ± 108.045  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1316.109     ± 73.440  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1299.063      ± 7.268  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47873.250     ± 49.195  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59945.585     ± 75.003  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51415.378    ± 639.779  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5592.595    ± 181.699  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6200.847     ± 96.529  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6168.708    ± 161.247  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        611.427      ± 5.887  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        534.977     ± 20.927  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5724.348   ± 1533.432  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2948.720    ± 284.581  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4508.289     ± 60.252  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     521837.321   ± 4957.459  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538124.782   ± 4656.054  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     549078.876   ± 3946.787  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     553425.704   ± 3006.837  ops/s
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
