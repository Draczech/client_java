# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-02T05:19:23Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.58K | ± 663.55 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.69K | ± 378.37 | ops/s | 1.2x slower |
| prometheusAdd | 50.61K | ± 1.18K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.46K | ± 702.86 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.70K | ± 18.74 | ops/s | 9.9x slower |
| simpleclientInc | 6.51K | ± 124.59 | ops/s | 10x slower |
| simpleclientAdd | 6.42K | ± 242.67 | ops/s | 10x slower |
| openTelemetryInc | 1.40K | ± 164.26 | ops/s | 48x slower |
| openTelemetryAdd | 1.24K | ± 75.35 | ops/s | 54x slower |
| openTelemetryIncNoLabels | 1.20K | ± 98.74 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.72K | ± 1.33K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 23.09 | ops/s | 1.3x slower |
| prometheusNative | 2.85K | ± 249.37 | ops/s | 2.0x slower |
| openTelemetryClassic | 686.51 | ± 51.02 | ops/s | 8.3x slower |
| openTelemetryExponential | 565.14 | ± 39.32 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.64K | ± 2.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.38K | ± 5.78K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.76K | ± 3.85K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.81K | ± 4.74K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49460.994    ± 702.858  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1235.273     ± 75.349  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1401.285    ± 164.264  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1195.983     ± 98.737  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50607.901   ± 1181.051  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66576.477    ± 663.554  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56689.037    ± 378.372  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6415.515    ± 242.666  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6506.843    ± 124.593  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6698.475     ± 18.744  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.513     ± 51.021  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.144     ± 39.319  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5720.262   ± 1327.740  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2851.608    ± 249.374  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4542.995     ± 23.086  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466807.785   ± 4737.982  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475759.423   ± 3852.350  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481380.320   ± 5776.876  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488642.148   ± 2751.351  ops/s
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
