# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-06T07:01:07Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.18K | ± 3.24K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.71K | ± 394.04 | ops/s | 1.2x slower |
| prometheusAdd | 48.48K | ± 491.83 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.35K | ± 459.46 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.25K | ± 31.27 | ops/s | 9.5x slower |
| simpleclientInc | 6.11K | ± 166.49 | ops/s | 9.7x slower |
| simpleclientAdd | 6.07K | ± 102.62 | ops/s | 9.7x slower |
| openTelemetryAdd | 1.36K | ± 87.12 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.35K | ± 86.82 | ops/s | 44x slower |
| openTelemetryInc | 1.31K | ± 9.07 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.14K | ± 1.48K | ops/s | **fastest** |
| simpleclient | 4.15K | ± 35.07 | ops/s | 1.5x slower |
| prometheusNative | 3.04K | ± 166.11 | ops/s | 2.0x slower |
| openTelemetryClassic | 600.62 | ± 18.65 | ops/s | 10x slower |
| openTelemetryExponential | 517.73 | ± 16.08 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 542.21K | ± 3.78K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.81K | ± 7.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 522.34K | ± 3.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 510.87K | ± 4.65K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44345.881    ± 459.459  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1363.478     ± 87.115  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1306.953      ± 9.074  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1345.800     ± 86.823  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48477.314    ± 491.832  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59179.347   ± 3240.396  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50712.775    ± 394.042  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6070.019    ± 102.620  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6105.468    ± 166.486  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6249.117     ± 31.269  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        600.617     ± 18.655  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        517.730     ± 16.082  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6139.490   ± 1484.784  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3035.003    ± 166.107  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4152.043     ± 35.073  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     510872.892   ± 4653.458  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     522340.538   ± 3301.775  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524814.040   ± 7836.952  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     542210.208   ± 3776.709  ops/s
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
