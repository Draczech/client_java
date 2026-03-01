# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-01T05:27:59Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.30K | ± 6.33K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.53K | ± 1.04K | ops/s | 1.1x slower |
| prometheusAdd | 51.73K | ± 179.68 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.39K | ± 2.57K | ops/s | 1.3x slower |
| simpleclientInc | 6.62K | ± 186.58 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.54K | ± 219.99 | ops/s | 9.7x slower |
| simpleclientAdd | 6.25K | ± 240.63 | ops/s | 10x slower |
| openTelemetryAdd | 1.56K | ± 226.78 | ops/s | 41x slower |
| openTelemetryInc | 1.24K | ± 33.67 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.23K | ± 16.06 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.54K | ± 41.97 | ops/s | **fastest** |
| prometheusClassic | 4.40K | ± 798.75 | ops/s | 1.0x slower |
| prometheusNative | 2.63K | ± 78.57 | ops/s | 1.7x slower |
| openTelemetryClassic | 694.08 | ± 46.36 | ops/s | 6.5x slower |
| openTelemetryExponential | 531.53 | ± 5.80 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.53K | ± 1.50K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.04K | ± 2.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.33K | ± 1.66K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.93K | ± 5.60K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48386.051   ± 2573.208  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1559.295    ± 226.776  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1238.386     ± 33.668  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1230.989     ± 16.064  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51728.688    ± 179.676  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63304.600   ± 6334.215  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56526.426   ± 1043.872  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6247.234    ± 240.632  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6618.821    ± 186.577  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6538.991    ± 219.990  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        694.080     ± 46.359  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        531.527      ± 5.795  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4403.123    ± 798.750  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2626.362     ± 78.574  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4540.317     ± 41.965  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482929.091   ± 5604.207  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486327.225   ± 1658.152  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491044.006   ± 2422.245  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495533.889   ± 1497.459  ops/s
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
