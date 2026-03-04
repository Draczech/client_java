# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-04T05:13:42Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.36K | ± 1.51K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.00K | ± 417.21 | ops/s | 1.1x slower |
| prometheusAdd | 51.41K | ± 467.46 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.34K | ± 7.16K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 6.69K | ± 13.48 | ops/s | 9.8x slower |
| simpleclientInc | 6.62K | ± 172.28 | ops/s | 9.9x slower |
| simpleclientAdd | 6.38K | ± 234.61 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 259.65 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.33K | ± 172.74 | ops/s | 49x slower |
| openTelemetryInc | 1.25K | ± 4.63 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.55K | ± 1.01K | ops/s | **fastest** |
| simpleclient | 4.53K | ± 71.87 | ops/s | 1.4x slower |
| prometheusNative | 3.20K | ± 24.18 | ops/s | 2.0x slower |
| openTelemetryClassic | 694.93 | ± 18.62 | ops/s | 9.4x slower |
| openTelemetryExponential | 570.76 | ± 18.60 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.64K | ± 6.46K | ops/s | **fastest** |
| prometheusWriteToByteArray | 493.88K | ± 2.00K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 488.52K | ± 4.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.69K | ± 3.96K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43336.057   ± 7157.239  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1443.709    ± 259.652  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1252.775      ± 4.629  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1330.993    ± 172.740  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51411.684    ± 467.457  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65363.518   ± 1507.326  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56997.225    ± 417.212  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6377.337    ± 234.612  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6619.546    ± 172.281  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6687.422     ± 13.482  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        694.935     ± 18.623  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        570.761     ± 18.603  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6546.214   ± 1012.935  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3195.016     ± 24.178  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4526.538     ± 71.869  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488517.342   ± 4789.280  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487688.600   ± 3957.592  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493877.562   ± 2002.219  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502636.278   ± 6457.128  ops/s
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
