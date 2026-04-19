# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-19T05:57:38Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.79K | ± 1.62K | ops/s | **fastest** |
| prometheusAdd | 50.60K | ± 544.74 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.42K | ± 1.52K | ops/s | 1.3x slower |
| prometheusNoLabelsInc | 46.96K | ± 12.21K | ops/s | 1.4x slower |
| simpleclientInc | 6.52K | ± 198.93 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.45K | ± 151.29 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 205.47 | ops/s | 11x slower |
| openTelemetryAdd | 1.28K | ± 65.86 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.26K | ± 23.12 | ops/s | 52x slower |
| openTelemetryInc | 1.25K | ± 54.38 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.30K | ± 1.71K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 53.35 | ops/s | 1.2x slower |
| prometheusNative | 3.21K | ± 128.80 | ops/s | 1.6x slower |
| openTelemetryClassic | 676.32 | ± 24.78 | ops/s | 7.8x slower |
| openTelemetryExponential | 548.13 | ± 22.15 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.60K | ± 5.76K | ops/s | **fastest** |
| prometheusWriteToByteArray | 478.56K | ± 5.11K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.56K | ± 5.85K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.21K | ± 6.99K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49418.739   ± 1516.648  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1281.597     ± 65.863  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1247.543     ± 54.381  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1259.691     ± 23.118  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50596.798    ± 544.738  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65792.013   ± 1618.706  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      46961.505  ± 12212.880  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6204.535    ± 205.472  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6516.612    ± 198.935  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6447.548    ± 151.294  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        676.321     ± 24.780  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.132     ± 22.145  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5303.644   ± 1705.941  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3214.751    ± 128.804  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4453.803     ± 53.354  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472209.147   ± 6990.794  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478562.099   ± 5847.002  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     478562.498   ± 5107.150  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488596.873   ± 5757.129  ops/s
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
