# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-11T08:00:39Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.14K | ± 1.07K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.87K | ± 391.46 | ops/s | 1.1x slower |
| prometheusAdd | 50.79K | ± 1.46K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.07K | ± 128.70 | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 199.09 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.41K | ± 161.46 | ops/s | 10x slower |
| simpleclientAdd | 6.07K | ± 45.16 | ops/s | 11x slower |
| openTelemetryAdd | 1.49K | ± 156.54 | ops/s | 44x slower |
| openTelemetryInc | 1.37K | ± 240.31 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.19K | ± 63.52 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.13K | ± 559.67 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 34.28 | ops/s | 1.2x slower |
| prometheusNative | 2.79K | ± 89.91 | ops/s | 1.8x slower |
| openTelemetryClassic | 711.17 | ± 15.35 | ops/s | 7.2x slower |
| openTelemetryExponential | 560.44 | ± 14.13 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 471.56K | ± 3.59K | ops/s | **fastest** |
| prometheusWriteToByteArray | 466.25K | ± 6.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 457.05K | ± 4.08K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 451.75K | ± 4.89K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50071.678    ± 128.705  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1488.243    ± 156.544  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1374.354    ± 240.310  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1186.604     ± 63.522  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50792.085   ± 1462.789  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65137.003   ± 1066.787  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56873.534    ± 391.461  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6069.860     ± 45.159  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6562.813    ± 199.086  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6410.454    ± 161.459  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        711.167     ± 15.354  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.439     ± 14.130  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5129.730    ± 559.668  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2794.163     ± 89.912  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4445.122     ± 34.281  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     451750.485   ± 4893.465  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     457052.320   ± 4083.154  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     466251.308   ± 6632.175  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     471559.037   ± 3588.646  ops/s
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
