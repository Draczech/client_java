# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-20T06:04:33Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.57K | ± 1.89K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.53K | ± 1.14K | ops/s | 1.1x slower |
| prometheusAdd | 51.24K | ± 705.50 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.04K | ± 985.79 | ops/s | 1.3x slower |
| simpleclientInc | 6.67K | ± 67.84 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.41K | ± 104.53 | ops/s | 10x slower |
| simpleclientAdd | 6.13K | ± 227.82 | ops/s | 11x slower |
| openTelemetryInc | 1.27K | ± 22.41 | ops/s | 51x slower |
| openTelemetryAdd | 1.22K | ± 23.79 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.17K | ± 24.69 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.79K | ± 727.52 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 61.63 | ops/s | 1.1x slower |
| prometheusNative | 2.81K | ± 329.51 | ops/s | 1.7x slower |
| openTelemetryClassic | 708.55 | ± 9.43 | ops/s | 6.8x slower |
| openTelemetryExponential | 587.98 | ± 26.76 | ops/s | 8.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 477.51K | ± 5.40K | ops/s | **fastest** |
| prometheusWriteToByteArray | 469.20K | ± 5.17K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 466.19K | ± 3.31K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 459.24K | ± 4.32K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48041.023    ± 985.793  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1218.417     ± 23.790  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1267.050     ± 22.407  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1173.273     ± 24.691  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51243.220    ± 705.502  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64566.413   ± 1889.960  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56528.033   ± 1138.080  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6133.445    ± 227.816  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6666.783     ± 67.841  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6409.588    ± 104.528  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        708.546      ± 9.432  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        587.976     ± 26.759  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4792.273    ± 727.522  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2809.199    ± 329.510  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4462.035     ± 61.629  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459235.524   ± 4324.925  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     466193.527   ± 3309.693  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     469202.687   ± 5172.535  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     477510.128   ± 5404.580  ops/s
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
