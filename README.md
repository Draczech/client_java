# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-16T04:06:23Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.11K | ± 1.30K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.98K | ± 405.72 | ops/s | 1.1x slower |
| prometheusAdd | 51.41K | ± 158.23 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.37K | ± 1.03K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 65.70 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.35K | ± 224.89 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 174.25 | ops/s | 10x slower |
| openTelemetryAdd | 1.54K | ± 222.44 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.42K | ± 221.15 | ops/s | 46x slower |
| openTelemetryInc | 1.40K | ± 214.45 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.03K | ± 1.52K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 10.47 | ops/s | 1.1x slower |
| prometheusNative | 2.96K | ± 338.98 | ops/s | 1.7x slower |
| openTelemetryClassic | 715.06 | ± 47.14 | ops/s | 7.0x slower |
| openTelemetryExponential | 606.54 | ± 13.23 | ops/s | 8.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 468.46K | ± 2.73K | ops/s | **fastest** |
| openMetricsWriteToNull | 468.29K | ± 4.70K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 465.13K | ± 6.04K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 451.07K | ± 5.24K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49367.525   ± 1034.970  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1540.944    ± 222.436  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1401.112    ± 214.448  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1417.855    ± 221.151  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51409.699    ± 158.234  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65108.362   ± 1301.460  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56976.592    ± 405.717  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6306.004    ± 174.249  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6661.627     ± 65.702  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6350.372    ± 224.892  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        715.062     ± 47.143  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        606.541     ± 13.226  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5032.353   ± 1521.037  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2964.422    ± 338.976  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4503.693     ± 10.469  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     451074.390   ± 5240.320  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468287.152   ± 4700.985  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     465132.867   ± 6040.977  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     468455.404   ± 2734.320  ops/s
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
