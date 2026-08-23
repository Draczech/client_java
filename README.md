# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-23T04:08:53Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.44K | ± 1.76K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.55K | ± 451.32 | ops/s | 1.1x slower |
| prometheusAdd | 48.67K | ± 931.96 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.45K | ± 473.41 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.26K | ± 31.47 | ops/s | 9.2x slower |
| simpleclientInc | 6.21K | ± 139.33 | ops/s | 9.2x slower |
| simpleclientAdd | 5.84K | ± 323.26 | ops/s | 9.8x slower |
| openTelemetryInc | 1.41K | ± 156.46 | ops/s | 41x slower |
| openTelemetryAdd | 1.37K | ± 36.09 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.31K | ± 57.28 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.58K | ± 662.83 | ops/s | **fastest** |
| simpleclient | 4.30K | ± 49.66 | ops/s | 1.1x slower |
| prometheusNative | 3.15K | ± 30.26 | ops/s | 1.5x slower |
| openTelemetryClassic | 654.58 | ± 19.21 | ops/s | 7.0x slower |
| openTelemetryExponential | 515.31 | ± 17.77 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 557.11K | ± 4.98K | ops/s | **fastest** |
| prometheusWriteToByteArray | 548.01K | ± 3.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.79K | ± 2.77K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.41K | ± 4.13K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44447.472    ± 473.414  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1370.698     ± 36.095  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1406.377    ± 156.459  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1310.791     ± 57.278  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48673.312    ± 931.965  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57437.949   ± 1760.811  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51549.769    ± 451.318  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5842.830    ± 323.262  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6211.135    ± 139.333  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6260.587     ± 31.465  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        654.581     ± 19.210  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        515.312     ± 17.769  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4581.803    ± 662.828  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3154.835     ± 30.264  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4300.160     ± 49.665  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524413.020   ± 4129.691  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538786.036   ± 2767.541  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548011.040   ± 3681.934  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     557107.299   ± 4979.514  ops/s
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
