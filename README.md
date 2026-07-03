# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-03T06:56:51Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.58K | ± 1.70K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.91K | ± 326.94 | ops/s | 1.2x slower |
| prometheusAdd | 51.29K | ± 520.69 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.02K | ± 1.50K | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 19.34 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.49K | ± 188.19 | ops/s | 10x slower |
| simpleclientAdd | 6.15K | ± 218.39 | ops/s | 11x slower |
| openTelemetryAdd | 1.59K | ± 256.00 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.31K | ± 207.18 | ops/s | 50x slower |
| openTelemetryInc | 1.23K | ± 19.56 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.47K | ± 2.26K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 38.95 | ops/s | 1.5x slower |
| prometheusNative | 2.86K | ± 207.03 | ops/s | 2.3x slower |
| openTelemetryClassic | 673.87 | ± 41.24 | ops/s | 9.6x slower |
| openTelemetryExponential | 562.74 | ± 29.38 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 480.23K | ± 3.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 469.94K | ± 5.85K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.07K | ± 5.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 465.89K | ± 4.51K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49016.964   ± 1497.206  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1590.375    ± 256.002  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1233.904     ± 19.565  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1312.007    ± 207.180  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51290.504    ± 520.694  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65579.594   ± 1702.295  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56908.600    ± 326.939  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6147.152    ± 218.393  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6688.765     ± 19.338  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6490.984    ± 188.187  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        673.873     ± 41.235  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.743     ± 29.381  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6466.514   ± 2257.550  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2859.118    ± 207.032  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4427.190     ± 38.952  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469070.009   ± 5942.720  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     465887.313   ± 4511.844  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     469943.812   ± 5853.275  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     480225.733   ± 3486.387  ops/s
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
