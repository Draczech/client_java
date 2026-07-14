# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-14T05:53:56Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.47K | ± 552.30 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.17K | ± 1.31K | ops/s | 1.2x slower |
| prometheusAdd | 51.07K | ± 411.40 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.53K | ± 778.79 | ops/s | 1.4x slower |
| simpleclientInc | 6.70K | ± 12.11 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 228.93 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 209.30 | ops/s | 10x slower |
| openTelemetryAdd | 1.47K | ± 223.71 | ops/s | 45x slower |
| openTelemetryInc | 1.47K | ± 150.69 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.43K | ± 233.66 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.03K | ± 660.12 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 80.76 | ops/s | 1.4x slower |
| prometheusNative | 2.98K | ± 296.18 | ops/s | 2.0x slower |
| openTelemetryClassic | 719.15 | ± 46.10 | ops/s | 8.4x slower |
| openTelemetryExponential | 578.53 | ± 42.94 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 481.21K | ± 3.73K | ops/s | **fastest** |
| prometheusWriteToByteArray | 476.57K | ± 5.86K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.33K | ± 3.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 467.32K | ± 4.84K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47530.205    ± 778.787  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1474.810    ± 223.707  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1469.541    ± 150.689  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1434.797    ± 233.656  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51072.237    ± 411.405  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66471.905    ± 552.300  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56174.347   ± 1310.696  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6339.720    ± 209.296  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6703.680     ± 12.114  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6477.781    ± 228.934  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        719.153     ± 46.104  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        578.531     ± 42.936  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6025.795    ± 660.118  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2983.316    ± 296.183  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4409.333     ± 80.757  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471332.562   ± 3285.791  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     467324.969   ± 4840.579  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476569.615   ± 5856.576  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481211.639   ± 3733.463  ops/s
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
