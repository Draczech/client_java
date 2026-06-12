# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-12T07:39:06Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.23K | ± 670.18 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.17K | ± 1.06K | ops/s | 1.2x slower |
| prometheusAdd | 51.58K | ± 86.63 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.98K | ± 1.69K | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 56.38 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.35K | ± 152.17 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 237.21 | ops/s | 11x slower |
| openTelemetryAdd | 1.24K | ± 73.59 | ops/s | 53x slower |
| openTelemetryInc | 1.22K | ± 29.98 | ops/s | 54x slower |
| openTelemetryIncNoLabels | 1.18K | ± 45.73 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.50K | ± 1.07K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 69.38 | ops/s | 1.2x slower |
| prometheusNative | 3.00K | ± 296.36 | ops/s | 1.8x slower |
| openTelemetryClassic | 712.54 | ± 49.24 | ops/s | 7.7x slower |
| openTelemetryExponential | 558.39 | ± 31.14 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.26K | ± 2.33K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.38K | ± 6.73K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.76K | ± 2.23K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.60K | ± 4.42K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47977.036   ± 1689.066  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1244.807     ± 73.589  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1219.784     ± 29.981  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1180.737     ± 45.730  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51583.395     ± 86.629  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66232.695    ± 670.176  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56172.659   ± 1061.190  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6178.235    ± 237.207  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6661.748     ± 56.381  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6353.065    ± 152.168  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        712.537     ± 49.236  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.389     ± 31.139  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5496.475   ± 1065.811  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3003.403    ± 296.362  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.937     ± 69.378  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468596.438   ± 4424.507  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481756.658   ± 2230.751  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482376.391   ± 6729.241  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491263.313   ± 2329.348  ops/s
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
