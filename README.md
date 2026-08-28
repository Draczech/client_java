# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-28T14:43:51Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.44K | ± 1.37K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.66K | ± 889.78 | ops/s | 1.2x slower |
| prometheusAdd | 51.16K | ± 144.78 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.88K | ± 947.56 | ops/s | 1.4x slower |
| simpleclientInc | 6.70K | ± 8.36 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.59K | ± 10.95 | ops/s | 9.9x slower |
| simpleclientAdd | 6.26K | ± 220.94 | ops/s | 10x slower |
| openTelemetryAdd | 1.63K | ± 273.99 | ops/s | 40x slower |
| openTelemetryInc | 1.44K | ± 244.23 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.16K | ± 13.00 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.60K | ± 1.47K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 91.97 | ops/s | 1.3x slower |
| prometheusNative | 3.01K | ± 336.99 | ops/s | 1.9x slower |
| openTelemetryClassic | 656.30 | ± 15.62 | ops/s | 8.5x slower |
| openTelemetryExponential | 561.03 | ± 29.26 | ops/s | 10.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 469.85K | ± 14.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 461.19K | ± 7.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 453.13K | ± 3.31K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 449.21K | ± 3.34K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46883.363    ± 947.563  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1631.536    ± 273.994  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1435.389    ± 244.228  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1164.369     ± 12.995  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51159.080    ± 144.781  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65437.086   ± 1367.268  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56663.031    ± 889.776  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6255.727    ± 220.939  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6700.421      ± 8.363  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6594.079     ± 10.954  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        656.297     ± 15.619  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.027     ± 29.263  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5598.960   ± 1471.637  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3013.527    ± 336.992  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4415.261     ± 91.967  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     449213.702   ± 3344.921  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     453130.890   ± 3306.913  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     461187.025   ± 7785.882  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     469854.437  ± 14148.737  ops/s
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
