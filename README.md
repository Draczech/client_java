# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-14T06:55:17Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.13K | ± 1.86K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.87K | ± 331.35 | ops/s | 1.2x slower |
| prometheusAdd | 51.06K | ± 874.02 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.63K | ± 1.54K | ops/s | 1.3x slower |
| simpleclientInc | 6.46K | ± 200.72 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 193.51 | ops/s | 10x slower |
| simpleclientAdd | 6.22K | ± 389.91 | ops/s | 11x slower |
| openTelemetryAdd | 1.56K | ± 211.20 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.23K | ± 12.02 | ops/s | 54x slower |
| openTelemetryInc | 1.17K | ± 49.08 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.19K | ± 1.55K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 39.83 | ops/s | 1.4x slower |
| prometheusNative | 3.27K | ± 133.07 | ops/s | 1.9x slower |
| openTelemetryClassic | 666.79 | ± 22.26 | ops/s | 9.3x slower |
| openTelemetryExponential | 553.49 | ± 1.09 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.00K | ± 6.39K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.10K | ± 6.07K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.73K | ± 4.77K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.67K | ± 5.62K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49634.463   ± 1535.678  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1563.386    ± 211.196  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1171.144     ± 49.080  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1227.393     ± 12.022  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51055.059    ± 874.023  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66132.615   ± 1858.998  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56865.418    ± 331.347  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6218.864    ± 389.911  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6455.769    ± 200.724  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6399.158    ± 193.514  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        666.795     ± 22.264  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        553.492      ± 1.092  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6194.466   ± 1551.790  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3272.464    ± 133.073  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4398.659     ± 39.826  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473669.615   ± 5616.416  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483726.344   ± 4773.717  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485098.434   ± 6072.712  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493002.007   ± 6393.149  ops/s
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
