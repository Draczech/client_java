# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-11T07:04:21Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.22K | ± 299.16 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.14K | ± 1.25K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.51K | ± 1.17K | ops/s | 1.4x slower |
| prometheusAdd | 41.70K | ± 9.91K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.20K | ± 110.92 | ops/s | 9.6x slower |
| simpleclientInc | 6.18K | ± 158.74 | ops/s | 9.6x slower |
| simpleclientAdd | 6.15K | ± 58.69 | ops/s | 9.6x slower |
| openTelemetryInc | 1.36K | ± 76.71 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.35K | ± 70.08 | ops/s | 44x slower |
| openTelemetryAdd | 1.28K | ± 20.88 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.41K | ± 2.73K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 84.85 | ops/s | 1.5x slower |
| prometheusNative | 2.83K | ± 182.87 | ops/s | 2.3x slower |
| openTelemetryClassic | 613.62 | ± 20.83 | ops/s | 10x slower |
| openTelemetryExponential | 498.62 | ± 24.25 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 559.93K | ± 3.71K | ops/s | **fastest** |
| prometheusWriteToByteArray | 545.10K | ± 6.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 541.53K | ± 3.25K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 519.91K | ± 8.74K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43514.749   ± 1171.341  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1280.551     ± 20.878  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1356.370     ± 76.711  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1346.915     ± 70.082  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      41695.028   ± 9905.228  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59215.974    ± 299.158  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50142.594   ± 1253.138  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6145.700     ± 58.690  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6180.271    ± 158.741  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6198.861    ± 110.924  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        613.616     ± 20.829  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        498.623     ± 24.246  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6409.387   ± 2733.270  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2825.593    ± 182.866  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4390.610     ± 84.854  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     519912.928   ± 8736.088  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     541534.033   ± 3246.580  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     545104.483   ± 6923.029  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     559928.235   ± 3714.967  ops/s
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
