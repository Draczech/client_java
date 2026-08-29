# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-29T09:38:05Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.42K | ± 712.69 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.77K | ± 1.17K | ops/s | 1.2x slower |
| prometheusAdd | 50.86K | ± 243.71 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.86K | ± 1.35K | ops/s | 1.4x slower |
| simpleclientInc | 6.70K | ± 8.92 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.49K | ± 182.30 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 243.22 | ops/s | 11x slower |
| openTelemetryInc | 1.45K | ± 218.19 | ops/s | 46x slower |
| openTelemetryAdd | 1.40K | ± 237.39 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.16K | ± 73.84 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.67K | ± 500.79 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 64.38 | ops/s | 1.1x slower |
| prometheusNative | 2.82K | ± 228.04 | ops/s | 1.7x slower |
| openTelemetryClassic | 686.14 | ± 43.27 | ops/s | 6.8x slower |
| openTelemetryExponential | 555.36 | ± 36.72 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.23K | ± 1.86K | ops/s | **fastest** |
| openMetricsWriteToNull | 480.09K | ± 3.40K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 477.51K | ± 4.00K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.19K | ± 4.04K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48859.024   ± 1351.692  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1395.211    ± 237.386  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1449.034    ± 218.188  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1161.256     ± 73.842  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50857.985    ± 243.705  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66417.938    ± 712.692  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55769.638   ± 1165.300  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6162.768    ± 243.217  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6696.700      ± 8.924  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6485.938    ± 182.303  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.139     ± 43.267  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        555.361     ± 36.718  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4674.789    ± 500.786  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2815.869    ± 228.037  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4445.910     ± 64.376  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463186.890   ± 4039.076  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480090.310   ± 3400.716  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     477511.591   ± 3996.378  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489232.704   ± 1864.031  ops/s
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
