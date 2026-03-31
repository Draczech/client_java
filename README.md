# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-31T05:42:09Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.06K | ± 1.21K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.86K | ± 2.28K | ops/s | 1.2x slower |
| prometheusAdd | 51.35K | ± 322.62 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.73K | ± 1.21K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.47K | ± 203.34 | ops/s | 10x slower |
| simpleclientInc | 6.46K | ± 193.78 | ops/s | 10x slower |
| simpleclientAdd | 6.07K | ± 64.35 | ops/s | 11x slower |
| openTelemetryAdd | 1.42K | ± 212.80 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.21K | ± 18.79 | ops/s | 54x slower |
| openTelemetryInc | 1.21K | ± 54.23 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.47K | ± 64.21 | ops/s | **fastest** |
| prometheusClassic | 4.42K | ± 601.22 | ops/s | 1.0x slower |
| prometheusNative | 3.15K | ± 91.85 | ops/s | 1.4x slower |
| openTelemetryClassic | 700.33 | ± 48.30 | ops/s | 6.4x slower |
| openTelemetryExponential | 569.09 | ± 36.45 | ops/s | 7.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.56K | ± 1.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.88K | ± 1.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.37K | ± 1.03K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.24K | ± 4.40K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48731.806   ± 1205.134  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1419.081    ± 212.796  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1210.828     ± 54.229  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1214.069     ± 18.793  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51352.073    ± 322.619  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65056.920   ± 1212.033  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55855.684   ± 2283.339  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6068.663     ± 64.353  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6461.157    ± 193.783  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6471.404    ± 203.336  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        700.329     ± 48.296  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.088     ± 36.455  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4419.625    ± 601.224  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3151.525     ± 91.851  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4467.472     ± 64.214  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472238.265   ± 4403.950  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483371.271   ± 1025.331  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489876.323   ± 1804.593  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490560.107   ± 1152.851  ops/s
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
