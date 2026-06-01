# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-01T07:59:49Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.60K | ± 1.16K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.04K | ± 808.60 | ops/s | 1.2x slower |
| prometheusAdd | 47.82K | ± 565.59 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.85K | ± 1.47K | ops/s | 1.4x slower |
| simpleclientInc | 6.18K | ± 129.51 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 5.99K | ± 203.32 | ops/s | 10x slower |
| simpleclientAdd | 5.88K | ± 123.63 | ops/s | 10x slower |
| openTelemetryAdd | 1.42K | ± 45.28 | ops/s | 43x slower |
| openTelemetryInc | 1.36K | ± 103.98 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.26K | ± 94.11 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.76K | ± 365.16 | ops/s | **fastest** |
| simpleclient | 4.57K | ± 84.73 | ops/s | 1.0x slower |
| prometheusNative | 3.01K | ± 232.80 | ops/s | 1.6x slower |
| openTelemetryClassic | 629.70 | ± 15.72 | ops/s | 7.6x slower |
| openTelemetryExponential | 532.20 | ± 14.81 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.35K | ± 5.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 539.74K | ± 1.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.83K | ± 4.67K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 521.75K | ± 2.10K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44852.758   ± 1465.181  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1420.136     ± 45.279  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1359.112    ± 103.981  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1261.171     ± 94.110  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47818.731    ± 565.587  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60600.017   ± 1162.391  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51040.583    ± 808.602  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5879.827    ± 123.629  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6176.315    ± 129.507  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5989.461    ± 203.320  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        629.702     ± 15.716  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        532.205     ± 14.812  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4760.444    ± 365.162  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3010.340    ± 232.797  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4571.224     ± 84.731  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     521751.153   ± 2101.690  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534832.345   ± 4668.470  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     539738.263   ± 1291.685  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555347.124   ± 5494.933  ops/s
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
