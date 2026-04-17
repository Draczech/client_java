# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-17T05:55:34Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.05K | ± 1.84K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.15K | ± 142.78 | ops/s | 1.2x slower |
| prometheusAdd | 51.58K | ± 100.01 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 40.86K | ± 10.43K | ops/s | 1.6x slower |
| simpleclientInc | 6.65K | ± 62.49 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.49K | ± 186.25 | ops/s | 10x slower |
| simpleclientAdd | 5.96K | ± 77.60 | ops/s | 11x slower |
| openTelemetryInc | 1.37K | ± 197.81 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.33K | ± 159.73 | ops/s | 50x slower |
| openTelemetryAdd | 1.27K | ± 10.35 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.53K | ± 2.03K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 31.62 | ops/s | 1.3x slower |
| prometheusNative | 3.01K | ± 345.89 | ops/s | 1.8x slower |
| openTelemetryClassic | 682.98 | ± 23.78 | ops/s | 8.1x slower |
| openTelemetryExponential | 590.89 | ± 4.79 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.98K | ± 2.16K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.89K | ± 5.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.30K | ± 3.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.04K | ± 3.31K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40862.943  ± 10428.358  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1272.058     ± 10.353  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1372.365    ± 197.810  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1325.829    ± 159.729  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51579.599    ± 100.008  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66048.136   ± 1838.595  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57153.315    ± 142.785  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5956.337     ± 77.601  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6650.507     ± 62.487  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6487.887    ± 186.247  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.983     ± 23.785  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        590.889      ± 4.790  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5533.443   ± 2029.130  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3005.946    ± 345.886  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4421.277     ± 31.617  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466042.539   ± 3309.123  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475299.177   ± 3304.900  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479886.470   ± 5229.954  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488980.188   ± 2158.979  ops/s
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
