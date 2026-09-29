# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-29T08:52:13Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.90K | ± 388.02 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.95K | ± 1.05K | ops/s | 1.2x slower |
| prometheusAdd | 51.50K | ± 116.76 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.39K | ± 1.46K | ops/s | 1.4x slower |
| simpleclientInc | 6.68K | ± 22.54 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.45K | ± 199.64 | ops/s | 10x slower |
| simpleclientAdd | 6.12K | ± 296.92 | ops/s | 11x slower |
| openTelemetryAdd | 1.50K | ± 236.59 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.31K | ± 148.57 | ops/s | 51x slower |
| openTelemetryInc | 1.30K | ± 140.40 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.28K | ± 1.36K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 34.78 | ops/s | 1.2x slower |
| prometheusNative | 3.01K | ± 335.95 | ops/s | 1.8x slower |
| openTelemetryClassic | 657.41 | ± 10.71 | ops/s | 8.0x slower |
| openTelemetryExponential | 564.10 | ± 22.94 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.45K | ± 3.99K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.80K | ± 3.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.47K | ± 2.28K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.83K | ± 3.10K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48392.000   ± 1463.088  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1503.587    ± 236.588  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1303.627    ± 140.402  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1314.612    ± 148.573  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51503.761    ± 116.762  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66896.878    ± 388.020  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55951.236   ± 1053.078  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6116.531    ± 296.916  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6675.632     ± 22.540  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6448.581    ± 199.640  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        657.408     ± 10.710  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        564.103     ± 22.940  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5283.622   ± 1362.570  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3007.576    ± 335.954  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4426.476     ± 34.776  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476826.101   ± 3101.390  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485468.351   ± 2283.087  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488803.474   ± 3426.428  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491447.542   ± 3989.226  ops/s
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
