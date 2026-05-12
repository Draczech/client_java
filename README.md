# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-12T06:45:22Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.46K | ± 2.22K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.73K | ± 1.87K | ops/s | 1.2x slower |
| prometheusAdd | 51.62K | ± 54.60 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.75K | ± 870.08 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.60K | ± 23.07 | ops/s | 9.8x slower |
| simpleclientInc | 6.53K | ± 235.48 | ops/s | 9.9x slower |
| simpleclientAdd | 6.08K | ± 330.50 | ops/s | 11x slower |
| openTelemetryAdd | 1.36K | ± 77.49 | ops/s | 47x slower |
| openTelemetryInc | 1.23K | ± 7.58 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.19K | ± 41.18 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.94K | ± 1.34K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 79.69 | ops/s | 1.4x slower |
| prometheusNative | 2.74K | ± 249.19 | ops/s | 2.2x slower |
| openTelemetryClassic | 691.52 | ± 34.08 | ops/s | 8.6x slower |
| openTelemetryExponential | 567.70 | ± 9.16 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.12K | ± 2.56K | ops/s | **fastest** |
| prometheusWriteToByteArray | 478.30K | ± 4.73K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 459.70K | ± 3.79K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 459.16K | ± 3.54K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49752.277    ± 870.085  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1361.225     ± 77.489  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1226.373      ± 7.579  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1189.065     ± 41.179  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51619.946     ± 54.597  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64458.889   ± 2221.270  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52729.211   ± 1870.043  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6080.268    ± 330.496  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6530.067    ± 235.476  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6603.379     ± 23.072  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.523     ± 34.076  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.704      ± 9.163  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5943.327   ± 1339.737  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2744.948    ± 249.189  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4398.322     ± 79.686  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459699.099   ± 3793.328  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     459158.339   ± 3539.455  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     478297.739   ± 4729.243  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484120.109   ± 2560.334  ops/s
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
