# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-24T07:12:52Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.85K | ± 1.71K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.45K | ± 1.12K | ops/s | 1.2x slower |
| prometheusAdd | 51.22K | ± 211.64 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.80K | ± 8.37K | ops/s | 1.5x slower |
| simpleclientInc | 6.52K | ± 199.09 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.30K | ± 68.88 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 153.50 | ops/s | 11x slower |
| openTelemetryAdd | 1.43K | ± 164.24 | ops/s | 46x slower |
| openTelemetryInc | 1.25K | ± 63.17 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.22K | ± 23.86 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.16K | ± 567.71 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 26.88 | ops/s | 1.1x slower |
| prometheusNative | 3.15K | ± 113.29 | ops/s | 1.6x slower |
| openTelemetryClassic | 678.87 | ± 35.50 | ops/s | 7.6x slower |
| openTelemetryExponential | 546.62 | ± 33.03 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.74K | ± 1.48K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.23K | ± 3.03K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.65K | ± 5.75K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.46K | ± 14.40K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44800.999   ± 8371.942  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1432.996    ± 164.239  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1248.063     ± 63.172  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1220.196     ± 23.861  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51218.617    ± 211.642  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65854.728   ± 1708.672  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56453.328   ± 1122.437  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6202.321    ± 153.502  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6521.419    ± 199.092  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6299.304     ± 68.879  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        678.866     ± 35.503  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.625     ± 33.033  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5164.484    ± 567.713  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3149.668    ± 113.288  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4500.213     ± 26.880  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469460.301  ± 14400.713  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479646.615   ± 5745.753  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488226.979   ± 3034.273  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492743.879   ± 1480.060  ops/s
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
