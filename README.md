# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-12T06:29:29Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.20K | ± 1.54K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.48K | ± 67.22 | ops/s | 1.2x slower |
| prometheusAdd | 51.21K | ± 478.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.86K | ± 1.18K | ops/s | 1.4x slower |
| simpleclientInc | 6.54K | ± 210.84 | ops/s | 10.0x slower |
| simpleclientAdd | 6.48K | ± 21.55 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.47K | ± 223.59 | ops/s | 10x slower |
| openTelemetryInc | 1.51K | ± 201.87 | ops/s | 43x slower |
| openTelemetryAdd | 1.31K | ± 36.45 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.29K | ± 123.73 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 465.38 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 76.46 | ops/s | 1.2x slower |
| prometheusNative | 2.99K | ± 275.07 | ops/s | 1.8x slower |
| openTelemetryClassic | 684.48 | ± 39.85 | ops/s | 7.7x slower |
| openTelemetryExponential | 575.81 | ± 7.37 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToByteArray | 472.83K | ± 8.13K | ops/s | **fastest** |
| openMetricsWriteToNull | 422.92K | ± 31.79K | ops/s | 1.1x slower |
| prometheusWriteToNull | 421.19K | ± 5.64K | ops/s | 1.1x slower |
| prometheusWriteToByteArray | 415.98K | ± 6.04K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47857.797   ± 1181.288  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1311.614     ± 36.454  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1511.399    ± 201.868  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1294.103    ± 123.733  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51212.494    ± 478.380  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65199.182   ± 1535.291  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56480.859     ± 67.225  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6479.397     ± 21.551  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6544.899    ± 210.844  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6466.173    ± 223.594  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        684.483     ± 39.852  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.810      ± 7.373  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5290.060    ± 465.384  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2991.466    ± 275.070  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4418.228     ± 76.460  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472834.732   ± 8128.350  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     422917.060  ± 31788.331  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     415979.724   ± 6035.047  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     421193.243   ± 5637.451  ops/s
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
