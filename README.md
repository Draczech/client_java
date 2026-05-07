# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-07T06:36:57Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.87K | ± 1.72K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.74K | ± 481.59 | ops/s | 1.1x slower |
| prometheusAdd | 51.27K | ± 241.77 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.28K | ± 895.24 | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 63.83 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.48K | ± 197.88 | ops/s | 10x slower |
| simpleclientAdd | 6.01K | ± 71.28 | ops/s | 11x slower |
| openTelemetryAdd | 1.48K | ± 261.07 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.30K | ± 48.68 | ops/s | 50x slower |
| openTelemetryInc | 1.18K | ± 27.19 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.06K | ± 1.47K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 35.37 | ops/s | 1.4x slower |
| prometheusNative | 3.05K | ± 251.33 | ops/s | 2.0x slower |
| openTelemetryClassic | 707.13 | ± 33.23 | ops/s | 8.6x slower |
| openTelemetryExponential | 575.30 | ± 25.62 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 480.12K | ± 3.04K | ops/s | **fastest** |
| openMetricsWriteToNull | 473.74K | ± 8.06K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.55K | ± 3.43K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 469.66K | ± 6.02K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49280.514    ± 895.239  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1476.428    ± 261.073  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1176.670     ± 27.192  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1298.889     ± 48.682  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51269.046    ± 241.773  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64865.229   ± 1720.882  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56743.554    ± 481.586  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6006.864     ± 71.279  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6658.684     ± 63.826  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6478.318    ± 197.885  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        707.134     ± 33.230  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.297     ± 25.622  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6060.246   ± 1468.777  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3049.851    ± 251.335  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4397.160     ± 35.369  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472552.959   ± 3426.738  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473737.708   ± 8059.840  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     469658.701   ± 6016.775  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     480119.353   ± 3043.756  ops/s
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
