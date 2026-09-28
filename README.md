# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-28T09:06:12Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.25K | ± 278.68 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.12K | ± 239.60 | ops/s | 1.2x slower |
| prometheusAdd | 50.91K | ± 220.60 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.87K | ± 596.76 | ops/s | 1.3x slower |
| simpleclientInc | 6.47K | ± 177.00 | ops/s | 10x slower |
| simpleclientAdd | 6.37K | ± 98.36 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.33K | ± 158.45 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.40K | ± 141.65 | ops/s | 47x slower |
| openTelemetryInc | 1.34K | ± 157.31 | ops/s | 49x slower |
| openTelemetryAdd | 1.27K | ± 72.92 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.57K | ± 1.65K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 20.08 | ops/s | 1.2x slower |
| prometheusNative | 2.77K | ± 384.78 | ops/s | 2.0x slower |
| openTelemetryClassic | 652.74 | ± 20.70 | ops/s | 8.5x slower |
| openTelemetryExponential | 558.18 | ± 18.07 | ops/s | 10.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.24K | ± 4.11K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.97K | ± 1.62K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.53K | ± 3.40K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.05K | ± 2.10K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49869.008    ± 596.756  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1270.581     ± 72.916  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1343.281    ± 157.310  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1396.061    ± 141.645  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50909.865    ± 220.605  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66245.590    ± 278.678  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57122.935    ± 239.603  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6374.175     ± 98.356  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6472.276    ± 176.998  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6329.224    ± 158.455  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        652.738     ± 20.699  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.176     ± 18.069  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5566.108   ± 1648.751  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2766.492    ± 384.778  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4472.761     ± 20.083  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470048.568   ± 2101.354  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478526.474   ± 3398.000  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480972.403   ± 1622.433  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490242.902   ± 4113.308  ops/s
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
