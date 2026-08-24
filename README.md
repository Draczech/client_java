# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-24T04:09:50Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.50K | ± 586.93 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.15K | ± 524.18 | ops/s | 1.1x slower |
| prometheusAdd | 48.39K | ± 665.87 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.48K | ± 1.70K | ops/s | 1.4x slower |
| simpleclientInc | 6.22K | ± 121.42 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 5.99K | ± 238.96 | ops/s | 9.9x slower |
| simpleclientAdd | 5.81K | ± 263.20 | ops/s | 10x slower |
| openTelemetryAdd | 1.46K | ± 102.84 | ops/s | 41x slower |
| openTelemetryInc | 1.45K | ± 102.12 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.31K | ± 112.21 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.97K | ± 1.99K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 93.12 | ops/s | 1.5x slower |
| prometheusNative | 3.14K | ± 167.17 | ops/s | 2.2x slower |
| openTelemetryClassic | 616.51 | ± 22.69 | ops/s | 11x slower |
| openTelemetryExponential | 527.00 | ± 17.64 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 560.05K | ± 4.67K | ops/s | **fastest** |
| prometheusWriteToByteArray | 547.91K | ± 5.50K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 537.39K | ± 2.96K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 526.28K | ± 2.72K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43481.661   ± 1696.152  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1462.832    ± 102.840  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1452.790    ± 102.123  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1306.145    ± 112.210  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48386.989    ± 665.866  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59502.013    ± 586.935  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52146.306    ± 524.179  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5806.737    ± 263.199  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6217.075    ± 121.424  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5992.160    ± 238.959  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        616.506     ± 22.688  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        526.999     ± 17.636  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6973.894   ± 1987.126  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3136.486    ± 167.167  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4519.515     ± 93.116  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     526281.927   ± 2718.591  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     537389.174   ± 2962.570  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     547907.894   ± 5499.154  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     560046.980   ± 4669.717  ops/s
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
