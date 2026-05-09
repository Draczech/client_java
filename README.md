# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-09T06:15:06Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.57K | ± 1.57K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.93K | ± 224.51 | ops/s | 1.1x slower |
| prometheusAdd | 51.43K | ± 133.29 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.28K | ± 89.82 | ops/s | 1.4x slower |
| simpleclientInc | 6.55K | ± 206.64 | ops/s | 9.9x slower |
| simpleclientAdd | 6.46K | ± 34.36 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.43K | ± 145.15 | ops/s | 10x slower |
| openTelemetryAdd | 1.26K | ± 67.10 | ops/s | 51x slower |
| openTelemetryInc | 1.23K | ± 30.29 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.20K | ± 44.66 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.04K | ± 1.81K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 27.92 | ops/s | 1.4x slower |
| prometheusNative | 3.15K | ± 99.47 | ops/s | 1.9x slower |
| openTelemetryClassic | 693.16 | ± 35.13 | ops/s | 8.7x slower |
| openTelemetryExponential | 559.45 | ± 9.48 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.50K | ± 1.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 492.74K | ± 3.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.04K | ± 6.46K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.51K | ± 4.54K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47275.819     ± 89.824  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1263.699     ± 67.098  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1226.915     ± 30.289  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1203.031     ± 44.665  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51433.528    ± 133.287  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64566.796   ± 1569.436  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56934.027    ± 224.509  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6458.980     ± 34.364  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6549.553    ± 206.639  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6434.469    ± 145.150  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        693.163     ± 35.130  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.445      ± 9.476  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6040.876   ± 1812.294  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3151.051     ± 99.473  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4429.201     ± 27.919  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474505.109   ± 4540.394  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485039.817   ± 6458.731  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492738.153   ± 3131.814  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495502.100   ± 1940.661  ops/s
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
