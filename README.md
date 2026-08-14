# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-14T05:10:00Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.63K | ± 1.36K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.81K | ± 272.70 | ops/s | 1.2x slower |
| prometheusAdd | 51.14K | ± 361.99 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.26K | ± 1.54K | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 195.74 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.47K | ± 203.58 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 213.33 | ops/s | 11x slower |
| openTelemetryAdd | 1.42K | ± 264.29 | ops/s | 46x slower |
| openTelemetryInc | 1.36K | ± 137.62 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.36K | ± 180.83 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.20K | ± 1.85K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 76.24 | ops/s | 1.2x slower |
| prometheusNative | 2.73K | ± 338.35 | ops/s | 1.9x slower |
| openTelemetryClassic | 676.84 | ± 32.52 | ops/s | 7.7x slower |
| openTelemetryExponential | 606.41 | ± 15.87 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 487.49K | ± 2.69K | ops/s | **fastest** |
| prometheusWriteToByteArray | 483.59K | ± 4.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.37K | ± 6.13K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.44K | ± 16.69K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49256.130   ± 1536.253  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1421.818    ± 264.289  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1356.648    ± 137.622  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1355.588    ± 180.826  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51138.850    ± 361.993  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65632.765   ± 1363.877  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56812.626    ± 272.704  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6192.417    ± 213.325  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6575.294    ± 195.738  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6470.877    ± 203.583  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        676.840     ± 32.516  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        606.411     ± 15.866  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5196.730   ± 1848.144  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2734.148    ± 338.353  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4457.191     ± 76.236  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468435.534  ± 16688.106  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478374.739   ± 6128.129  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483588.999   ± 4119.111  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487487.188   ± 2692.149  ops/s
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
