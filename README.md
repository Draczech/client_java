# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-22T08:13:24Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.01K | ± 2.92K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.11K | ± 75.86 | ops/s | 1.1x slower |
| prometheusAdd | 51.40K | ± 210.16 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 50.19K | ± 1.01K | ops/s | 1.2x slower |
| simpleclientInc | 6.71K | ± 12.46 | ops/s | 8.9x slower |
| simpleclientNoLabelsInc | 6.22K | ± 34.02 | ops/s | 9.7x slower |
| simpleclientAdd | 5.90K | ± 160.18 | ops/s | 10x slower |
| openTelemetryAdd | 1.62K | ± 319.40 | ops/s | 37x slower |
| openTelemetryInc | 1.48K | ± 173.12 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.36K | ± 159.69 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.95K | ± 1.08K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 106.04 | ops/s | 1.3x slower |
| prometheusNative | 2.61K | ± 92.47 | ops/s | 2.3x slower |
| openTelemetryClassic | 701.51 | ± 39.46 | ops/s | 8.5x slower |
| openTelemetryExponential | 538.79 | ± 18.88 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 481.95K | ± 5.53K | ops/s | **fastest** |
| prometheusWriteToByteArray | 472.68K | ± 6.51K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 470.90K | ± 1.72K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.26K | ± 8.99K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50186.889   ± 1013.903  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1618.567    ± 319.399  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1480.524    ± 173.117  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1358.429    ± 159.691  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51403.405    ± 210.163  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60014.225   ± 2922.900  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57107.656     ± 75.864  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5904.566    ± 160.182  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6713.557     ± 12.463  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6218.035     ± 34.016  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        701.515     ± 39.459  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        538.793     ± 18.876  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5954.549   ± 1077.975  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2609.143     ± 92.474  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4460.329    ± 106.035  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463262.669   ± 8992.738  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470895.016   ± 1717.591  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     472679.909   ± 6511.699  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481945.958   ± 5531.774  ops/s
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
