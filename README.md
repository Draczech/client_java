# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-15T03:58:28Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 54.44K | ± 1.21K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.52K | ± 442.95 | ops/s | 1.1x slower |
| prometheusAdd | 48.39K | ± 414.32 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 42.48K | ± 1.26K | ops/s | 1.3x slower |
| simpleclientInc | 6.29K | ± 79.33 | ops/s | 8.7x slower |
| simpleclientNoLabelsInc | 5.98K | ± 212.81 | ops/s | 9.1x slower |
| simpleclientAdd | 5.77K | ± 106.31 | ops/s | 9.4x slower |
| openTelemetryIncNoLabels | 1.45K | ± 159.63 | ops/s | 38x slower |
| openTelemetryAdd | 1.43K | ± 142.16 | ops/s | 38x slower |
| openTelemetryInc | 1.41K | ± 55.42 | ops/s | 39x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.62K | ± 1.52K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 68.15 | ops/s | 1.3x slower |
| prometheusNative | 2.86K | ± 217.31 | ops/s | 2.0x slower |
| openTelemetryClassic | 587.26 | ± 5.35 | ops/s | 9.6x slower |
| openTelemetryExponential | 526.49 | ± 2.54 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 554.81K | ± 12.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 544.88K | ± 6.85K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 532.87K | ± 4.74K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.84K | ± 2.15K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42476.795   ± 1259.621  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1432.143    ± 142.164  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1408.172     ± 55.421  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1451.188    ± 159.628  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48391.916    ± 414.323  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      54442.585   ± 1210.317  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51519.740    ± 442.952  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5774.278    ± 106.308  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6285.324     ± 79.330  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5982.824    ± 212.813  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        587.258      ± 5.347  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        526.495      ± 2.541  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5619.610   ± 1520.952  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2862.992    ± 217.314  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4479.417     ± 68.149  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524839.082   ± 2153.481  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     532868.681   ± 4742.640  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     544877.941   ± 6848.248  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     554812.743  ± 12893.734  ops/s
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
