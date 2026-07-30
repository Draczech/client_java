# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-30T06:00:40Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.57K | ± 1.67K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.97K | ± 559.08 | ops/s | 1.2x slower |
| prometheusAdd | 51.36K | ± 389.45 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.11K | ± 1.67K | ops/s | 1.3x slower |
| simpleclientInc | 6.60K | ± 154.38 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.58K | ± 19.86 | ops/s | 10.0x slower |
| simpleclientAdd | 6.41K | ± 114.92 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.49K | ± 56.19 | ops/s | 44x slower |
| openTelemetryInc | 1.41K | ± 272.66 | ops/s | 47x slower |
| openTelemetryAdd | 1.32K | ± 63.97 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.05K | ± 667.94 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 56.71 | ops/s | 1.4x slower |
| prometheusNative | 3.03K | ± 192.04 | ops/s | 2.0x slower |
| openTelemetryClassic | 742.35 | ± 36.34 | ops/s | 8.2x slower |
| openTelemetryExponential | 590.05 | ± 30.87 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.77K | ± 3.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 470.75K | ± 6.86K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 467.74K | ± 2.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 459.73K | ± 16.82K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49114.003   ± 1666.363  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1323.126     ± 63.970  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1409.192    ± 272.657  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1489.889     ± 56.195  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51357.409    ± 389.449  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65571.469   ± 1672.832  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56966.373    ± 559.084  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6407.296    ± 114.919  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6597.214    ± 154.378  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6579.689     ± 19.861  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        742.346     ± 36.340  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        590.055     ± 30.870  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6053.972    ± 667.940  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3033.354    ± 192.035  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4453.684     ± 56.708  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459729.529  ± 16824.261  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     467735.328   ± 2605.291  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     470746.640   ± 6862.875  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485767.836   ± 3167.369  ops/s
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
