# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-18T07:17:56Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.84K | ± 1.71K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.48K | ± 842.03 | ops/s | 1.2x slower |
| prometheusAdd | 51.25K | ± 242.59 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.59K | ± 1.62K | ops/s | 1.3x slower |
| simpleclientInc | 6.57K | ± 155.05 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.51K | ± 137.66 | ops/s | 10x slower |
| simpleclientAdd | 6.47K | ± 34.42 | ops/s | 10x slower |
| openTelemetryInc | 1.44K | ± 233.16 | ops/s | 46x slower |
| openTelemetryAdd | 1.25K | ± 24.58 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.18K | ± 87.68 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.63K | ± 1.48K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 49.93 | ops/s | 1.3x slower |
| prometheusNative | 3.14K | ± 70.37 | ops/s | 1.8x slower |
| openTelemetryClassic | 675.61 | ± 17.51 | ops/s | 8.3x slower |
| openTelemetryExponential | 526.11 | ± 45.26 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.85K | ± 2.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.10K | ± 1.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.02K | ± 3.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.24K | ± 3.92K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49588.887   ± 1621.126  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1247.540     ± 24.585  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1439.105    ± 233.158  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1179.583     ± 87.683  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51245.853    ± 242.587  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65836.457   ± 1709.916  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56481.073    ± 842.030  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6466.678     ± 34.422  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6573.756    ± 155.048  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6512.753    ± 137.665  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        675.610     ± 17.510  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        526.111     ± 45.259  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5625.703   ± 1479.279  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3144.436     ± 70.371  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4473.309     ± 49.934  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475243.544   ± 3922.618  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476017.293   ± 3123.241  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488102.949   ± 1077.975  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491846.980   ± 2493.064  ops/s
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
