# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-04T06:08:23Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.59K | ± 1.42K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.64K | ± 329.00 | ops/s | 1.1x slower |
| prometheusAdd | 51.42K | ± 212.95 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.81K | ± 1.27K | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 224.46 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.44K | ± 200.63 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 345.20 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.36K | ± 158.72 | ops/s | 48x slower |
| openTelemetryAdd | 1.26K | ± 3.81 | ops/s | 51x slower |
| openTelemetryInc | 1.24K | ± 29.38 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.67K | ± 1.31K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 59.38 | ops/s | 1.3x slower |
| prometheusNative | 2.82K | ± 321.89 | ops/s | 2.0x slower |
| openTelemetryClassic | 663.70 | ± 22.46 | ops/s | 8.5x slower |
| openTelemetryExponential | 595.05 | ± 27.70 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 483.51K | ± 2.96K | ops/s | **fastest** |
| prometheusWriteToByteArray | 476.72K | ± 6.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.10K | ± 3.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.87K | ± 5.71K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49811.830   ± 1265.776  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1262.787      ± 3.808  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1240.061     ± 29.375  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1355.509    ± 158.720  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51424.134    ± 212.947  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64588.157   ± 1416.106  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56635.687    ± 328.996  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6202.693    ± 345.195  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6557.053    ± 224.460  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6435.171    ± 200.627  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        663.703     ± 22.462  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        595.053     ± 27.702  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5667.343   ± 1309.052  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2820.329    ± 321.891  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4475.778     ± 59.380  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472871.497   ± 5707.726  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473098.520   ± 3806.786  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476718.158   ± 6416.844  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     483509.270   ± 2956.846  ops/s
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
