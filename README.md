# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-06T06:08:38Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.82K | ± 657.53 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.75K | ± 748.29 | ops/s | 1.2x slower |
| prometheusAdd | 48.01K | ± 202.03 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.93K | ± 153.43 | ops/s | 1.4x slower |
| simpleclientAdd | 6.15K | ± 54.90 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.11K | ± 182.10 | ops/s | 10.0x slower |
| simpleclientInc | 6.09K | ± 227.74 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.53K | ± 168.86 | ops/s | 40x slower |
| openTelemetryInc | 1.46K | ± 94.79 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.31K | ± 101.16 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.70K | ± 794.17 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 60.90 | ops/s | 1.1x slower |
| prometheusNative | 3.00K | ± 131.64 | ops/s | 1.6x slower |
| openTelemetryClassic | 613.62 | ± 25.22 | ops/s | 7.7x slower |
| openTelemetryExponential | 553.53 | ± 9.72 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 539.46K | ± 9.24K | ops/s | **fastest** |
| prometheusWriteToByteArray | 519.02K | ± 5.86K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 513.07K | ± 5.03K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 499.90K | ± 9.39K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43925.692    ± 153.434  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1526.216    ± 168.855  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1462.521     ± 94.793  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1311.710    ± 101.162  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48005.831    ± 202.030  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60819.494    ± 657.526  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51752.200    ± 748.287  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6147.295     ± 54.895  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6087.657    ± 227.735  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6112.259    ± 182.099  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        613.620     ± 25.220  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        553.531      ± 9.719  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4702.217    ± 794.171  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3002.582    ± 131.645  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4377.419     ± 60.896  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     499900.623   ± 9393.118  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     513074.462   ± 5027.251  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     519017.923   ± 5862.169  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     539456.972   ± 9235.925  ops/s
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
