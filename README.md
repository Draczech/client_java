# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-03T07:58:35Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.79K | ± 477.33 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.77K | ± 330.17 | ops/s | 1.2x slower |
| prometheusAdd | 51.25K | ± 300.60 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.56K | ± 494.97 | ops/s | 1.3x slower |
| simpleclientInc | 6.47K | ± 93.40 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.39K | ± 168.18 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 220.20 | ops/s | 11x slower |
| openTelemetryAdd | 1.32K | ± 259.56 | ops/s | 50x slower |
| openTelemetryInc | 1.29K | ± 2.04 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.27K | ± 89.11 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.07K | ± 1.23K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 8.19 | ops/s | 1.4x slower |
| prometheusNative | 2.75K | ± 258.06 | ops/s | 2.2x slower |
| openTelemetryClassic | 660.63 | ± 45.42 | ops/s | 9.2x slower |
| openTelemetryExponential | 552.26 | ± 21.90 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.20K | ± 4.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.81K | ± 7.99K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.33K | ± 2.11K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.96K | ± 3.57K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49562.340    ± 494.971  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1324.660    ± 259.560  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1294.910      ± 2.043  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1267.857     ± 89.112  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51249.690    ± 300.602  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66791.469    ± 477.329  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56770.435    ± 330.165  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6176.749    ± 220.205  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6469.080     ± 93.396  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6391.836    ± 168.178  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        660.626     ± 45.423  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        552.264     ± 21.902  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6073.324   ± 1231.201  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2746.862    ± 258.059  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4385.348      ± 8.192  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470960.648   ± 3568.682  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478329.753   ± 2108.629  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481813.249   ± 7993.620  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488203.979   ± 4791.119  ops/s
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
