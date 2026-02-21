# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-21T05:12:27Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.20K | ± 2.00K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.18K | ± 755.17 | ops/s | 1.2x slower |
| prometheusAdd | 51.17K | ± 1.03K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.60K | ± 7.31K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 6.70K | ± 16.55 | ops/s | 9.7x slower |
| simpleclientInc | 6.68K | ± 140.30 | ops/s | 9.8x slower |
| simpleclientAdd | 6.53K | ± 33.20 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.34K | ± 65.41 | ops/s | 49x slower |
| openTelemetryInc | 1.28K | ± 145.09 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.21K | ± 77.47 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.51K | ± 25.33 | ops/s | **fastest** |
| prometheusClassic | 4.37K | ± 373.03 | ops/s | 1.0x slower |
| prometheusNative | 3.07K | ± 274.70 | ops/s | 1.5x slower |
| openTelemetryClassic | 687.06 | ± 56.01 | ops/s | 6.6x slower |
| openTelemetryExponential | 538.06 | ± 56.26 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 501.69K | ± 1.10K | ops/s | **fastest** |
| prometheusWriteToByteArray | 497.44K | ± 1.14K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 492.40K | ± 3.96K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 485.78K | ± 5.72K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43600.207   ± 7306.860  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1335.133     ± 65.409  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1275.652    ± 145.085  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1205.371     ± 77.472  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51165.273   ± 1027.056  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65198.745   ± 1995.318  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56180.873    ± 755.175  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6530.070     ± 33.200  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6682.163    ± 140.295  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6700.019     ± 16.551  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        687.064     ± 56.008  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        538.062     ± 56.260  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4373.228    ± 373.031  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3073.052    ± 274.702  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4510.545     ± 25.334  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485780.509   ± 5722.529  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     492400.636   ± 3955.921  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     497444.346   ± 1140.720  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     501691.261   ± 1099.951  ops/s
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
