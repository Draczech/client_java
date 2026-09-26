# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-26T08:01:24Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.44K | ± 586.90 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.29K | ± 1.03K | ops/s | 1.2x slower |
| prometheusAdd | 51.20K | ± 495.55 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.07K | ± 1.08K | ops/s | 1.4x slower |
| simpleclientInc | 6.62K | ± 56.34 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.49K | ± 196.32 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 229.77 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.34K | ± 113.43 | ops/s | 50x slower |
| openTelemetryAdd | 1.25K | ± 24.99 | ops/s | 53x slower |
| openTelemetryInc | 1.24K | ± 46.35 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.90K | ± 1.11K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 36.49 | ops/s | 1.3x slower |
| prometheusNative | 2.90K | ± 279.35 | ops/s | 2.0x slower |
| openTelemetryClassic | 676.78 | ± 25.91 | ops/s | 8.7x slower |
| openTelemetryExponential | 559.72 | ± 3.32 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.79K | ± 2.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 493.62K | ± 1.46K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.92K | ± 3.58K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.89K | ± 4.70K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49071.702   ± 1080.416  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1249.387     ± 24.985  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1241.990     ± 46.346  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1335.049    ± 113.428  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51195.053    ± 495.549  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66444.887    ± 586.901  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56292.006   ± 1034.846  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6296.361    ± 229.768  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6623.715     ± 56.344  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6492.877    ± 196.315  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        676.777     ± 25.905  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.721      ± 3.316  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5904.393   ± 1106.746  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2901.911    ± 279.350  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4464.159     ± 36.486  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483890.089   ± 4697.824  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488918.460   ± 3575.840  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493617.540   ± 1464.873  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496794.323   ± 2578.122  ops/s
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
