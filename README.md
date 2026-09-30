# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-30T08:52:17Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 77.25K | ± 111.59 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.08K | ± 1.25K | ops/s | 1.2x slower |
| prometheusAdd | 61.86K | ± 521.48 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 57.33K | ± 1.37K | ops/s | 1.3x slower |
| simpleclientInc | 7.97K | ± 135.98 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 7.85K | ± 297.98 | ops/s | 9.8x slower |
| simpleclientAdd | 7.77K | ± 270.22 | ops/s | 9.9x slower |
| openTelemetryInc | 1.93K | ± 89.70 | ops/s | 40x slower |
| openTelemetryAdd | 1.75K | ± 95.32 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.75K | ± 26.07 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.95K | ± 2.24K | ops/s | **fastest** |
| simpleclient | 5.88K | ± 64.50 | ops/s | 1.2x slower |
| prometheusNative | 3.67K | ± 244.72 | ops/s | 1.9x slower |
| openTelemetryClassic | 781.92 | ± 22.65 | ops/s | 8.9x slower |
| openTelemetryExponential | 651.20 | ± 51.75 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 678.30K | ± 4.81K | ops/s | **fastest** |
| prometheusWriteToByteArray | 658.95K | ± 10.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 646.77K | ± 4.33K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 631.15K | ± 6.91K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57328.007   ± 1368.114  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1753.147     ± 95.319  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1926.381     ± 89.700  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1747.635     ± 26.074  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61860.545    ± 521.479  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77253.349    ± 111.592  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66075.091   ± 1250.443  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7768.062    ± 270.224  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7970.623    ± 135.979  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7847.767    ± 297.983  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        781.916     ± 22.653  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        651.198     ± 51.748  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6949.382   ± 2238.962  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3671.111    ± 244.717  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5879.745     ± 64.504  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     631148.967   ± 6914.066  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     646767.665   ± 4329.743  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     658952.984  ± 10876.363  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     678298.645   ± 4809.051  ops/s
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
