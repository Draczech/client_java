# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-18T05:38:03Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.22K | ± 1.07K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.15K | ± 217.20 | ops/s | 1.1x slower |
| prometheusAdd | 51.41K | ± 289.09 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.60K | ± 1.34K | ops/s | 1.3x slower |
| simpleclientInc | 6.65K | ± 90.61 | ops/s | 9.7x slower |
| simpleclientAdd | 6.46K | ± 27.63 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.35K | ± 210.97 | ops/s | 10x slower |
| openTelemetryAdd | 1.40K | ± 138.38 | ops/s | 46x slower |
| openTelemetryInc | 1.32K | ± 165.22 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.16K | ± 42.19 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.56K | ± 1.19K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 66.59 | ops/s | 1.3x slower |
| prometheusNative | 2.91K | ± 368.60 | ops/s | 1.9x slower |
| openTelemetryClassic | 704.97 | ± 19.24 | ops/s | 7.9x slower |
| openTelemetryExponential | 551.65 | ± 13.05 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.18K | ± 5.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.30K | ± 2.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.62K | ± 3.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.28K | ± 4.64K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48598.295   ± 1336.364  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1397.301    ± 138.379  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1317.274    ± 165.221  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1163.358     ± 42.194  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51405.638    ± 289.091  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64219.174   ± 1070.384  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57154.029    ± 217.196  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6464.152     ± 27.627  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6649.586     ± 90.613  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6345.899    ± 210.969  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        704.971     ± 19.241  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.652     ± 13.054  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5557.936   ± 1188.069  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2914.877    ± 368.600  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4420.318     ± 66.588  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478621.783   ± 3668.518  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477279.283   ± 4639.820  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488299.853   ± 2096.872  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489175.484   ± 5012.202  ops/s
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
