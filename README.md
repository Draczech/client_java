# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-15T05:53:38Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.13K | ± 1.17K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.16K | ± 204.90 | ops/s | 1.1x slower |
| prometheusAdd | 51.44K | ± 242.03 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.38K | ± 2.15K | ops/s | 1.3x slower |
| simpleclientInc | 6.42K | ± 120.04 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.36K | ± 213.43 | ops/s | 10x slower |
| simpleclientAdd | 6.14K | ± 220.07 | ops/s | 10x slower |
| openTelemetryInc | 1.38K | ± 203.49 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.33K | ± 133.81 | ops/s | 48x slower |
| openTelemetryAdd | 1.26K | ± 32.92 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.69K | ± 553.77 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 104.12 | ops/s | 1.1x slower |
| prometheusNative | 2.93K | ± 259.58 | ops/s | 1.6x slower |
| openTelemetryClassic | 700.76 | ± 24.88 | ops/s | 6.7x slower |
| openTelemetryExponential | 550.49 | ± 29.41 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.91K | ± 4.51K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.54K | ± 5.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.05K | ± 3.89K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.36K | ± 2.73K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48380.944   ± 2150.877  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1257.655     ± 32.924  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1379.261    ± 203.494  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1331.533    ± 133.813  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51444.372    ± 242.028  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64131.186   ± 1166.688  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57159.747    ± 204.897  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6137.162    ± 220.074  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6422.801    ± 120.037  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6358.749    ± 213.433  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        700.762     ± 24.879  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.486     ± 29.413  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4688.773    ± 553.771  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2926.076    ± 259.579  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4405.152    ± 104.123  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468359.732   ± 2727.416  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475054.398   ± 3894.074  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480536.565   ± 5683.443  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485914.662   ± 4512.286  ops/s
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
