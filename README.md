# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-20T04:02:53Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 73.67K | ± 800.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 63.02K | ± 1.35K | ops/s | 1.2x slower |
| prometheusAdd | 58.00K | ± 1.43K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 53.36K | ± 760.26 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 7.71K | ± 328.35 | ops/s | 9.6x slower |
| simpleclientInc | 7.54K | ± 153.96 | ops/s | 9.8x slower |
| simpleclientAdd | 7.50K | ± 305.50 | ops/s | 9.8x slower |
| openTelemetryAdd | 1.85K | ± 125.58 | ops/s | 40x slower |
| openTelemetryInc | 1.81K | ± 184.35 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.66K | ± 249.45 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 8.86K | ± 627.53 | ops/s | **fastest** |
| simpleclient | 5.23K | ± 264.02 | ops/s | 1.7x slower |
| prometheusNative | 3.61K | ± 245.21 | ops/s | 2.5x slower |
| openTelemetryClassic | 793.38 | ± 28.06 | ops/s | 11x slower |
| openTelemetryExponential | 664.08 | ± 34.28 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 646.74K | ± 9.71K | ops/s | **fastest** |
| openMetricsWriteToNull | 630.86K | ± 3.96K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 626.08K | ± 12.84K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 608.97K | ± 3.84K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      53357.018    ± 760.258  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1845.304    ± 125.582  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1811.202    ± 184.346  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1662.771    ± 249.447  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      57999.922   ± 1427.633  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      73668.618    ± 800.518  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      63024.635   ± 1348.512  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7497.519    ± 305.502  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7535.229    ± 153.959  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7711.239    ± 328.348  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        793.381     ± 28.064  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        664.080     ± 34.277  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8864.195    ± 627.527  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3610.900    ± 245.206  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5231.880    ± 264.019  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     608965.610   ± 3841.680  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     630864.862   ± 3955.881  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     626077.136  ± 12841.643  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     646741.076   ± 9706.534  ops/s
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
