# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-02T07:02:38Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.99K | ± 1.04K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.56K | ± 1.09K | ops/s | 1.2x slower |
| prometheusAdd | 48.19K | ± 576.53 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 38.16K | ± 9.34K | ops/s | 1.6x slower |
| simpleclientInc | 6.19K | ± 97.67 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.12K | ± 244.58 | ops/s | 9.8x slower |
| simpleclientAdd | 5.99K | ± 139.66 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.53K | ± 88.38 | ops/s | 39x slower |
| openTelemetryInc | 1.40K | ± 25.77 | ops/s | 43x slower |
| openTelemetryAdd | 1.37K | ± 8.02 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.47K | ± 1.57K | ops/s | **fastest** |
| simpleclient | 4.26K | ± 99.29 | ops/s | 1.3x slower |
| prometheusNative | 3.21K | ± 109.80 | ops/s | 1.7x slower |
| openTelemetryClassic | 639.01 | ± 44.94 | ops/s | 8.6x slower |
| openTelemetryExponential | 518.67 | ± 30.08 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.96K | ± 6.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 543.14K | ± 3.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.76K | ± 2.18K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 521.64K | ± 11.52K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      38156.678   ± 9342.551  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1373.171      ± 8.020  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1400.942     ± 25.766  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1528.608     ± 88.378  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48192.069    ± 576.533  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59985.419   ± 1038.984  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51560.220   ± 1088.743  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5990.241    ± 139.663  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6190.612     ± 97.665  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6118.037    ± 244.580  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        639.005     ± 44.941  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        518.668     ± 30.081  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5474.167   ± 1573.910  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3206.396    ± 109.804  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4264.147     ± 99.292  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524756.095   ± 2175.204  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     521640.416  ± 11523.062  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     543135.268   ± 3808.074  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555961.357   ± 6012.630  ops/s
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
