# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-19T08:03:38Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.56K | ± 538.74 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.24K | ± 1.07K | ops/s | 1.2x slower |
| prometheusAdd | 48.43K | ± 143.47 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.05K | ± 1.17K | ops/s | 1.4x slower |
| simpleclientInc | 6.22K | ± 150.48 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 5.97K | ± 212.51 | ops/s | 10.0x slower |
| simpleclientAdd | 5.95K | ± 238.07 | ops/s | 10x slower |
| openTelemetryInc | 1.53K | ± 34.35 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.41K | ± 88.51 | ops/s | 42x slower |
| openTelemetryAdd | 1.30K | ± 9.21 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.87K | ± 1.23K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 35.38 | ops/s | 1.3x slower |
| prometheusNative | 3.07K | ± 162.05 | ops/s | 1.9x slower |
| openTelemetryClassic | 596.08 | ± 21.07 | ops/s | 9.8x slower |
| openTelemetryExponential | 515.54 | ± 14.32 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 559.73K | ± 2.18K | ops/s | **fastest** |
| prometheusWriteToByteArray | 549.16K | ± 5.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 536.37K | ± 2.60K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 526.28K | ± 6.98K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43051.639   ± 1172.254  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1303.452      ± 9.207  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1528.277     ± 34.346  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1408.226     ± 88.511  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48432.538    ± 143.471  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59560.011    ± 538.736  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51239.176   ± 1068.132  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5947.816    ± 238.074  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6219.164    ± 150.485  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5970.940    ± 212.507  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        596.084     ± 21.070  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        515.543     ± 14.319  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5867.445   ± 1233.913  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3069.914    ± 162.053  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4508.851     ± 35.381  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     526284.054   ± 6978.361  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     536365.367   ± 2598.500  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     549164.409   ± 5412.586  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     559730.890   ± 2181.297  ops/s
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
