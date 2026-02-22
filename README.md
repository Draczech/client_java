# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-22T05:22:27Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.37K | ± 1.68K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.55K | ± 1.15K | ops/s | 1.2x slower |
| prometheusAdd | 51.74K | ± 180.43 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.79K | ± 528.20 | ops/s | 1.3x slower |
| simpleclientInc | 6.78K | ± 25.29 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.71K | ± 11.58 | ops/s | 9.7x slower |
| simpleclientAdd | 6.44K | ± 175.14 | ops/s | 10x slower |
| openTelemetryAdd | 1.53K | ± 248.53 | ops/s | 43x slower |
| openTelemetryInc | 1.25K | ± 8.32 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.19K | ± 63.88 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.44K | ± 1.19K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 13.50 | ops/s | 1.2x slower |
| prometheusNative | 2.85K | ± 245.52 | ops/s | 1.9x slower |
| openTelemetryClassic | 689.48 | ± 21.87 | ops/s | 7.9x slower |
| openTelemetryExponential | 573.47 | ± 12.64 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 499.65K | ± 842.78 | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.10K | ± 1.93K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.33K | ± 9.76K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.33K | ± 5.72K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49790.681    ± 528.197  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1526.659    ± 248.527  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1245.898      ± 8.321  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1192.200     ± 63.882  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51742.531    ± 180.433  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65373.797   ± 1679.597  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56547.866   ± 1152.621  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6441.990    ± 175.137  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6775.301     ± 25.287  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6710.894     ± 11.583  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        689.485     ± 21.874  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        573.473     ± 12.641  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5438.412   ± 1188.068  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2845.319    ± 245.523  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4558.362     ± 13.500  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483326.247   ± 5720.311  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486327.378   ± 9764.627  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494103.258   ± 1926.901  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499653.433    ± 842.779  ops/s
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
