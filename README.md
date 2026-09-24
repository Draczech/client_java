# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-24T08:07:49Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.70K | ± 1.18K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.61K | ± 1.12K | ops/s | 1.2x slower |
| prometheusAdd | 48.26K | ± 263.69 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.80K | ± 828.32 | ops/s | 1.4x slower |
| simpleclientInc | 6.21K | ± 132.71 | ops/s | 9.6x slower |
| simpleclientAdd | 5.95K | ± 91.87 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.80K | ± 73.26 | ops/s | 10x slower |
| openTelemetryInc | 1.53K | ± 69.67 | ops/s | 39x slower |
| openTelemetryAdd | 1.49K | ± 89.50 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.34K | ± 91.85 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.70K | ± 1.49K | ops/s | **fastest** |
| simpleclient | 4.22K | ± 15.39 | ops/s | 1.4x slower |
| prometheusNative | 2.88K | ± 219.32 | ops/s | 2.0x slower |
| openTelemetryClassic | 661.42 | ± 14.29 | ops/s | 8.6x slower |
| openTelemetryExponential | 517.80 | ± 26.73 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 552.11K | ± 4.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 546.16K | ± 5.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 531.06K | ± 7.06K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 529.69K | ± 5.88K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43799.424    ± 828.323  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1485.398     ± 89.505  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1526.679     ± 69.668  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1338.528     ± 91.845  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48263.126    ± 263.689  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59704.158   ± 1184.785  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51609.755   ± 1119.121  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5948.393     ± 91.874  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6214.318    ± 132.713  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5798.857     ± 73.258  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        661.416     ± 14.288  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        517.795     ± 26.735  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5704.980   ± 1494.143  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2878.280    ± 219.322  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4217.831     ± 15.391  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     529687.634   ± 5879.756  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     531063.017   ± 7060.750  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     546163.146   ± 5265.546  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     552113.846   ± 4347.759  ops/s
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
