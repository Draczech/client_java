# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-17T08:07:10Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.74K | ± 969.14 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.94K | ± 417.38 | ops/s | 1.1x slower |
| prometheusAdd | 51.22K | ± 311.51 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.74K | ± 1.53K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 145.38 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 204.05 | ops/s | 10.0x slower |
| simpleclientAdd | 6.17K | ± 227.80 | ops/s | 10x slower |
| openTelemetryAdd | 1.28K | ± 67.50 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.21K | ± 23.47 | ops/s | 54x slower |
| openTelemetryInc | 1.19K | ± 7.59 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.82K | ± 714.99 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 68.11 | ops/s | 1.1x slower |
| prometheusNative | 2.80K | ± 310.08 | ops/s | 1.7x slower |
| openTelemetryClassic | 645.66 | ± 21.60 | ops/s | 7.5x slower |
| openTelemetryExponential | 522.64 | ± 20.93 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 480.34K | ± 5.47K | ops/s | **fastest** |
| prometheusWriteToByteArray | 471.54K | ± 5.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 462.00K | ± 5.34K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 455.35K | ± 6.72K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48737.514   ± 1526.936  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1275.904     ± 67.497  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1187.588      ± 7.593  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1206.227     ± 23.471  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51220.312    ± 311.514  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64738.268    ± 969.144  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56938.618    ± 417.381  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6173.045    ± 227.800  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6552.515    ± 145.376  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6481.332    ± 204.054  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        645.660     ± 21.601  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        522.644     ± 20.928  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4818.220    ± 714.988  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2795.561    ± 310.076  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4462.152     ± 68.105  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     455354.058   ± 6722.390  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     462004.168   ± 5338.836  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     471544.577   ± 5296.282  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     480337.394   ± 5468.531  ops/s
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
