# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-10T07:27:45Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.27K | ± 1.04K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.08K | ± 157.91 | ops/s | 1.1x slower |
| prometheusAdd | 51.36K | ± 195.73 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.24K | ± 775.60 | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 175.66 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.40K | ± 178.13 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 254.41 | ops/s | 10x slower |
| openTelemetryAdd | 1.45K | ± 236.94 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.26K | ± 177.50 | ops/s | 52x slower |
| openTelemetryInc | 1.24K | ± 49.81 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.68K | ± 1.50K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 52.09 | ops/s | 1.3x slower |
| prometheusNative | 3.23K | ± 131.35 | ops/s | 1.8x slower |
| openTelemetryClassic | 717.78 | ± 49.66 | ops/s | 7.9x slower |
| openTelemetryExponential | 544.87 | ± 26.18 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 471.85K | ± 4.31K | ops/s | **fastest** |
| openMetricsWriteToNull | 469.44K | ± 11.32K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 465.66K | ± 2.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 461.12K | ± 3.72K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48243.534    ± 775.602  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1446.543    ± 236.942  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1239.987     ± 49.805  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1257.792    ± 177.497  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51359.719    ± 195.735  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65267.053   ± 1038.003  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57080.902    ± 157.906  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6319.865    ± 254.405  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6586.602    ± 175.658  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6396.324    ± 178.128  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        717.777     ± 49.665  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.867     ± 26.184  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5678.470   ± 1498.415  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3226.310    ± 131.351  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4432.998     ± 52.088  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     461116.916   ± 3718.279  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     469439.463  ± 11317.410  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     465662.198   ± 2121.828  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     471854.107   ± 4308.867  ops/s
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
