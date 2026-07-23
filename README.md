# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-23T06:28:20Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 77.46K | ± 1.30K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.36K | ± 462.65 | ops/s | 1.2x slower |
| prometheusAdd | 61.63K | ± 402.40 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 57.49K | ± 712.43 | ops/s | 1.3x slower |
| simpleclientInc | 8.15K | ± 34.52 | ops/s | 9.5x slower |
| simpleclientAdd | 7.83K | ± 235.75 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 7.79K | ± 414.91 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.83K | ± 71.19 | ops/s | 42x slower |
| openTelemetryInc | 1.76K | ± 82.41 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.59K | ± 81.56 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.90K | ± 116.86 | ops/s | **fastest** |
| prometheusClassic | 5.02K | ± 59.86 | ops/s | 1.2x slower |
| prometheusNative | 3.66K | ± 312.64 | ops/s | 1.6x slower |
| openTelemetryClassic | 761.71 | ± 23.08 | ops/s | 7.7x slower |
| openTelemetryExponential | 677.92 | ± 12.06 | ops/s | 8.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 676.47K | ± 15.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 663.96K | ± 10.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 657.22K | ± 4.97K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 633.36K | ± 1.94K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57486.348    ± 712.428  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1827.785     ± 71.186  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1762.454     ± 82.405  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1586.886     ± 81.561  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61630.321    ± 402.397  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77459.059   ± 1298.001  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66355.773    ± 462.653  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7825.158    ± 235.754  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8146.839     ± 34.519  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7787.797    ± 414.913  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        761.714     ± 23.080  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        677.921     ± 12.064  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5016.506     ± 59.859  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3662.076    ± 312.643  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5902.277    ± 116.863  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     633363.416   ± 1936.908  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     657222.902   ± 4970.320  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     663957.418  ± 10077.712  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     676469.368  ± 15486.735  ops/s
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
