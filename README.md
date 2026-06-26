# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-26T07:14:58Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 75.56K | ± 2.65K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.49K | ± 591.21 | ops/s | 1.1x slower |
| prometheusAdd | 62.37K | ± 990.76 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.05K | ± 866.58 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 7.85K | ± 329.66 | ops/s | 9.6x slower |
| simpleclientAdd | 7.83K | ± 239.91 | ops/s | 9.7x slower |
| simpleclientInc | 7.70K | ± 194.79 | ops/s | 9.8x slower |
| openTelemetryAdd | 1.85K | ± 102.80 | ops/s | 41x slower |
| openTelemetryInc | 1.78K | ± 107.65 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.63K | ± 116.37 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.14K | ± 1.36K | ops/s | **fastest** |
| simpleclient | 5.70K | ± 253.94 | ops/s | 1.3x slower |
| prometheusNative | 3.99K | ± 150.53 | ops/s | 1.8x slower |
| openTelemetryClassic | 799.02 | ± 19.49 | ops/s | 8.9x slower |
| openTelemetryExponential | 644.19 | ± 22.47 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 671.58K | ± 3.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 659.00K | ± 8.05K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 645.71K | ± 7.82K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 637.62K | ± 5.00K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56052.023    ± 866.579  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1850.709    ± 102.803  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1781.189    ± 107.646  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1625.767    ± 116.371  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62369.922    ± 990.758  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75555.124   ± 2646.166  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66486.969    ± 591.209  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7826.843    ± 239.910  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7695.119    ± 194.792  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7847.831    ± 329.657  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        799.019     ± 19.487  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        644.187     ± 22.472  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7135.917   ± 1358.864  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3988.183    ± 150.526  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5704.761    ± 253.943  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     637617.334   ± 5003.591  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     645709.968   ± 7815.044  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     658996.611   ± 8049.668  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     671576.312   ± 3752.491  ops/s
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
