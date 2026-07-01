# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-01T07:31:09Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.61K | ± 454.39 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.78K | ± 259.81 | ops/s | 1.2x slower |
| prometheusAdd | 51.10K | ± 751.96 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.91K | ± 1.09K | ops/s | 1.4x slower |
| simpleclientInc | 6.62K | ± 145.58 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.60K | ± 6.23 | ops/s | 10x slower |
| simpleclientAdd | 6.01K | ± 20.59 | ops/s | 11x slower |
| openTelemetryInc | 1.64K | ± 333.51 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.25K | ± 22.83 | ops/s | 53x slower |
| openTelemetryAdd | 1.24K | ± 50.34 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.61K | ± 1.82K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 70.31 | ops/s | 1.5x slower |
| prometheusNative | 2.85K | ± 380.29 | ops/s | 2.3x slower |
| openTelemetryClassic | 683.00 | ± 60.51 | ops/s | 9.7x slower |
| openTelemetryExponential | 562.72 | ± 24.94 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 482.12K | ± 1.87K | ops/s | **fastest** |
| prometheusWriteToNull | 477.88K | ± 5.90K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.90K | ± 5.50K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 466.94K | ± 5.19K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47905.449   ± 1091.281  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1240.630     ± 50.339  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1639.973    ± 333.506  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1250.791     ± 22.830  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51104.822    ± 751.964  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66612.600    ± 454.388  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56777.031    ± 259.812  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6006.718     ± 20.595  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6617.510    ± 145.578  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6603.645      ± 6.230  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.004     ± 60.515  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.718     ± 24.936  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6607.772   ± 1820.727  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2854.634    ± 380.285  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4459.610     ± 70.312  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467899.616   ± 5497.307  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     466940.137   ± 5186.731  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482119.237   ± 1874.079  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     477883.857   ± 5898.892  ops/s
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
