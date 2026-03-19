# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-19T05:27:19Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.44K | ± 844.82 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.11K | ± 390.10 | ops/s | 1.2x slower |
| prometheusAdd | 51.78K | ± 211.18 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.83K | ± 2.21K | ops/s | 1.4x slower |
| simpleclientInc | 6.78K | ± 27.29 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.59K | ± 168.13 | ops/s | 10x slower |
| simpleclientAdd | 6.42K | ± 172.18 | ops/s | 10x slower |
| openTelemetryAdd | 1.46K | ± 308.24 | ops/s | 46x slower |
| openTelemetryInc | 1.40K | ± 209.38 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.22K | ± 32.17 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.79K | ± 1.23K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 42.10 | ops/s | 1.3x slower |
| prometheusNative | 3.04K | ± 271.32 | ops/s | 1.9x slower |
| openTelemetryClassic | 682.56 | ± 42.83 | ops/s | 8.5x slower |
| openTelemetryExponential | 557.63 | ± 25.90 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.49K | ± 1.03K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.27K | ± 4.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.84K | ± 4.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.64K | ± 4.14K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48828.881   ± 2212.717  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1456.376    ± 308.244  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1395.310    ± 209.385  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1218.799     ± 32.165  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51784.979    ± 211.178  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66437.233    ± 844.816  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57113.527    ± 390.097  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6417.984    ± 172.178  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6783.031     ± 27.291  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6590.218    ± 168.134  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.561     ± 42.828  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.626     ± 25.898  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5790.421   ± 1226.629  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3042.082    ± 271.322  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4501.088     ± 42.101  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473638.946   ± 4139.808  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483836.618   ± 4880.006  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487266.248   ± 4793.455  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496491.742   ± 1028.638  ops/s
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
