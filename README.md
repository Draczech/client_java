# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-23T08:07:35Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.16K | ± 1.09K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.04K | ± 292.40 | ops/s | 1.1x slower |
| prometheusAdd | 51.32K | ± 212.39 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.42K | ± 1.20K | ops/s | 1.3x slower |
| simpleclientInc | 6.54K | ± 148.92 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.38K | ± 175.33 | ops/s | 10x slower |
| simpleclientAdd | 6.24K | ± 186.26 | ops/s | 10x slower |
| openTelemetryInc | 1.49K | ± 100.58 | ops/s | 44x slower |
| openTelemetryAdd | 1.40K | ± 259.22 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.21K | ± 31.27 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.01K | ± 1.42K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 68.57 | ops/s | 1.4x slower |
| prometheusNative | 2.80K | ± 325.88 | ops/s | 2.1x slower |
| openTelemetryClassic | 699.39 | ± 44.79 | ops/s | 8.6x slower |
| openTelemetryExponential | 532.64 | ± 26.41 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 477.75K | ± 7.08K | ops/s | **fastest** |
| prometheusWriteToByteArray | 468.05K | ± 8.25K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 460.88K | ± 5.18K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 451.46K | ± 7.63K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49418.168   ± 1200.741  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1396.013    ± 259.221  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1493.274    ± 100.585  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1208.311     ± 31.267  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51320.962    ± 212.387  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65155.226   ± 1093.647  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57043.631    ± 292.403  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6236.127    ± 186.263  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6539.908    ± 148.921  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6382.238    ± 175.331  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        699.388     ± 44.793  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        532.644     ± 26.410  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6005.909   ± 1421.104  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2795.061    ± 325.882  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4448.159     ± 68.568  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     460882.157   ± 5179.558  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     451458.762   ± 7633.874  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     468052.756   ± 8253.731  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     477748.408   ± 7079.482  ops/s
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
