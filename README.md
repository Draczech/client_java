# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-09T05:39:01Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.34K | ± 764.67 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.94K | ± 2.07K | ops/s | 1.2x slower |
| prometheusAdd | 48.01K | ± 317.92 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.04K | ± 213.74 | ops/s | 1.4x slower |
| simpleclientInc | 6.21K | ± 192.98 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.00K | ± 230.99 | ops/s | 10x slower |
| simpleclientAdd | 6.00K | ± 126.42 | ops/s | 10x slower |
| openTelemetryInc | 1.47K | ± 136.44 | ops/s | 41x slower |
| openTelemetryAdd | 1.39K | ± 147.49 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.35K | ± 59.12 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.68K | ± 1.27K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 140.23 | ops/s | 1.5x slower |
| prometheusNative | 2.98K | ± 215.70 | ops/s | 2.2x slower |
| openTelemetryClassic | 605.58 | ± 26.07 | ops/s | 11x slower |
| openTelemetryExponential | 557.70 | ± 23.56 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 554.36K | ± 5.78K | ops/s | **fastest** |
| prometheusWriteToByteArray | 539.16K | ± 7.09K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 537.53K | ± 5.49K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 526.11K | ± 2.45K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44036.122    ± 213.738  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1388.235    ± 147.490  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1473.377    ± 136.443  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1354.909     ± 59.123  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48007.784    ± 317.915  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60337.287    ± 764.666  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50940.770   ± 2070.258  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6002.248    ± 126.424  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6214.046    ± 192.981  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6004.335    ± 230.987  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        605.580     ± 26.070  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.699     ± 23.559  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6679.870   ± 1274.995  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2977.817    ± 215.700  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4443.912    ± 140.231  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     526114.970   ± 2452.215  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     537528.368   ± 5486.693  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     539156.217   ± 7092.814  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     554359.324   ± 5777.007  ops/s
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
