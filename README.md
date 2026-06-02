# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-02T07:42:18Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.21K | ± 1.46K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.12K | ± 916.60 | ops/s | 1.2x slower |
| prometheusAdd | 51.61K | ± 95.07 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.74K | ± 2.11K | ops/s | 1.3x slower |
| simpleclientInc | 6.68K | ± 15.88 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.36K | ± 34.87 | ops/s | 10x slower |
| simpleclientAdd | 5.94K | ± 107.86 | ops/s | 11x slower |
| openTelemetryAdd | 1.41K | ± 190.77 | ops/s | 46x slower |
| openTelemetryInc | 1.33K | ± 201.53 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.29K | ± 137.34 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.55K | ± 1.58K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 50.54 | ops/s | 1.3x slower |
| prometheusNative | 3.21K | ± 48.69 | ops/s | 1.7x slower |
| openTelemetryClassic | 694.66 | ± 24.41 | ops/s | 8.0x slower |
| openTelemetryExponential | 551.36 | ± 26.16 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.59K | ± 2.16K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.30K | ± 2.86K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.75K | ± 3.72K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 462.83K | ± 11.33K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49744.947   ± 2110.560  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1412.901    ± 190.770  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1334.798    ± 201.529  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1291.613    ± 137.345  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51611.078     ± 95.069  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65205.874   ± 1455.597  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56123.300    ± 916.601  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5935.380    ± 107.856  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6680.809     ± 15.877  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6357.403     ± 34.873  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        694.655     ± 24.412  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.357     ± 26.162  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5547.046   ± 1582.972  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3208.996     ± 48.687  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4437.570     ± 50.543  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     462828.244  ± 11331.720  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477751.548   ± 3719.386  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487299.566   ± 2861.995  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489592.080   ± 2156.012  ops/s
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
