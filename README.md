# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-15T05:52:22Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.80K | ± 1.90K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.02K | ± 565.94 | ops/s | 1.2x slower |
| prometheusAdd | 51.03K | ± 607.06 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.30K | ± 1.58K | ops/s | 1.4x slower |
| simpleclientInc | 6.69K | ± 24.06 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.51K | ± 93.44 | ops/s | 10x slower |
| simpleclientAdd | 6.48K | ± 24.84 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 204.25 | ops/s | 48x slower |
| openTelemetryAdd | 1.32K | ± 118.37 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.22K | ± 46.10 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.66K | ± 1.49K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 40.70 | ops/s | 1.3x slower |
| prometheusNative | 2.95K | ± 315.43 | ops/s | 1.9x slower |
| openTelemetryClassic | 648.22 | ± 32.06 | ops/s | 8.7x slower |
| openTelemetryExponential | 585.89 | ± 16.28 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.48K | ± 2.14K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.77K | ± 2.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.71K | ± 2.14K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.44K | ± 1.23K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48299.209   ± 1575.624  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1316.719    ± 118.366  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1364.151    ± 204.247  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1215.535     ± 46.101  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51032.580    ± 607.062  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65796.856   ± 1896.337  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57016.725    ± 565.941  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6478.881     ± 24.841  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6685.738     ± 24.061  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6514.874     ± 93.441  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        648.219     ± 32.063  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        585.894     ± 16.285  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5660.757   ± 1486.495  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2953.457    ± 315.432  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4477.777     ± 40.702  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471444.561   ± 1230.742  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477714.331   ± 2144.315  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486772.173   ± 2669.159  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488476.475   ± 2141.888  ops/s
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
