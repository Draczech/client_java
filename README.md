# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-04T06:49:40Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 78.62K | ± 1.05K | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.51K | ± 389.14 | ops/s | 1.2x slower |
| prometheusAdd | 63.80K | ± 604.15 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.95K | ± 889.67 | ops/s | 1.4x slower |
| simpleclientInc | 8.12K | ± 41.13 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 7.90K | ± 328.39 | ops/s | 9.9x slower |
| simpleclientAdd | 7.77K | ± 203.35 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.86K | ± 93.25 | ops/s | 42x slower |
| openTelemetryInc | 1.84K | ± 146.50 | ops/s | 43x slower |
| openTelemetryAdd | 1.73K | ± 21.96 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.75K | ± 2.87K | ops/s | **fastest** |
| simpleclient | 5.61K | ± 37.02 | ops/s | 1.2x slower |
| prometheusNative | 3.81K | ± 221.40 | ops/s | 1.8x slower |
| openTelemetryClassic | 785.42 | ± 11.93 | ops/s | 8.6x slower |
| openTelemetryExponential | 685.83 | ± 19.42 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 673.61K | ± 5.06K | ops/s | **fastest** |
| prometheusWriteToByteArray | 653.07K | ± 6.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 647.02K | ± 3.09K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 636.08K | ± 7.40K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56949.887    ± 889.672  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1728.238     ± 21.963  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1844.178    ± 146.505  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1857.193     ± 93.251  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63804.604    ± 604.155  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      78619.148   ± 1048.848  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65513.971    ± 389.142  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7773.397    ± 203.353  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8117.907     ± 41.125  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7903.520    ± 328.389  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        785.425     ± 11.929  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        685.831     ± 19.424  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6750.615   ± 2868.258  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3809.418    ± 221.403  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5609.278     ± 37.016  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     636082.717   ± 7395.308  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     647015.586   ± 3087.619  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     653067.328   ± 6242.895  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     673608.287   ± 5063.808  ops/s
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
