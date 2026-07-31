# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-31T06:37:52Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.61K | ± 1.56K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.08K | ± 101.98 | ops/s | 1.1x slower |
| prometheusAdd | 51.16K | ± 661.16 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.38K | ± 616.24 | ops/s | 1.3x slower |
| simpleclientInc | 6.42K | ± 71.17 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.35K | ± 198.80 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 378.73 | ops/s | 11x slower |
| openTelemetryInc | 1.37K | ± 188.08 | ops/s | 48x slower |
| openTelemetryAdd | 1.35K | ± 205.45 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.33K | ± 193.07 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.13K | ± 1.42K | ops/s | **fastest** |
| simpleclient | 4.49K | ± 35.47 | ops/s | 1.1x slower |
| prometheusNative | 2.82K | ± 385.48 | ops/s | 1.8x slower |
| openTelemetryClassic | 679.56 | ± 28.64 | ops/s | 7.6x slower |
| openTelemetryExponential | 560.86 | ± 18.94 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.39K | ± 7.83K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.39K | ± 2.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 472.06K | ± 3.22K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.76K | ± 6.79K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50379.568    ± 616.237  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1353.864    ± 205.452  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1366.708    ± 188.084  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1325.717    ± 193.074  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51155.784    ± 661.162  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65608.716   ± 1560.364  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57077.439    ± 101.981  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6212.844    ± 378.734  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6418.553     ± 71.168  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6346.019    ± 198.797  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.558     ± 28.640  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.863     ± 18.939  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5132.173   ± 1421.100  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2817.983    ± 385.475  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4485.700     ± 35.467  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464762.917   ± 6794.112  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     472057.467   ± 3219.111  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479392.284   ± 2665.196  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484388.963   ± 7834.910  ops/s
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
