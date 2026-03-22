# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-22T05:24:56Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.59K | ± 1.71K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.80K | ± 403.35 | ops/s | 1.2x slower |
| prometheusAdd | 51.47K | ± 654.81 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.77K | ± 864.64 | ops/s | 1.4x slower |
| simpleclientInc | 6.64K | ± 182.04 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.60K | ± 140.75 | ops/s | 9.9x slower |
| simpleclientAdd | 6.40K | ± 157.20 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 231.11 | ops/s | 48x slower |
| openTelemetryAdd | 1.28K | ± 41.23 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.21K | ± 15.25 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.34K | ± 1.31K | ops/s | **fastest** |
| simpleclient | 4.57K | ± 21.91 | ops/s | 1.4x slower |
| prometheusNative | 2.98K | ± 335.16 | ops/s | 2.1x slower |
| openTelemetryClassic | 692.79 | ± 27.61 | ops/s | 9.2x slower |
| openTelemetryExponential | 578.19 | ± 27.80 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.34K | ± 6.57K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.10K | ± 3.89K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.48K | ± 10.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.61K | ± 7.23K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47773.862    ± 864.639  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1276.613     ± 41.228  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1363.205    ± 231.111  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1208.872     ± 15.249  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51474.551    ± 654.807  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65591.907   ± 1705.450  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56804.226    ± 403.345  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6395.809    ± 157.198  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6643.266    ± 182.038  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6599.619    ± 140.749  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        692.785     ± 27.610  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        578.194     ± 27.804  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6342.997   ± 1313.174  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2982.123    ± 335.162  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4565.571     ± 21.913  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472614.636   ± 7228.490  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479475.037  ± 10611.211  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488104.909   ± 3885.810  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492341.360   ± 6565.772  ops/s
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
