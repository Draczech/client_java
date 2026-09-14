# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-14T08:33:11Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.32K | ± 1.23K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.01K | ± 1.21K | ops/s | 1.2x slower |
| prometheusAdd | 51.15K | ± 339.73 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.49K | ± 1.48K | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 168.74 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.43K | ± 173.38 | ops/s | 10x slower |
| simpleclientAdd | 6.29K | ± 272.85 | ops/s | 10x slower |
| openTelemetryAdd | 1.40K | ± 202.73 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.40K | ± 217.05 | ops/s | 47x slower |
| openTelemetryInc | 1.27K | ± 7.37 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.52K | ± 1.20K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 158.23 | ops/s | 1.3x slower |
| prometheusNative | 3.01K | ± 302.30 | ops/s | 1.8x slower |
| openTelemetryClassic | 685.19 | ± 46.57 | ops/s | 8.1x slower |
| openTelemetryExponential | 582.04 | ± 42.50 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 499.18K | ± 7.14K | ops/s | **fastest** |
| prometheusWriteToByteArray | 496.84K | ± 5.39K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 490.75K | ± 2.21K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 486.27K | ± 7.42K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48490.861   ± 1476.413  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1402.315    ± 202.730  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1268.085      ± 7.372  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1399.771    ± 217.046  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51152.532    ± 339.729  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65320.912   ± 1231.088  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56007.556   ± 1205.360  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6294.151    ± 272.853  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6530.254    ± 168.744  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6431.328    ± 173.383  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        685.193     ± 46.572  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        582.042     ± 42.499  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5521.115   ± 1200.790  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3014.971    ± 302.296  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4408.035    ± 158.230  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486271.581   ± 7417.180  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490746.063   ± 2212.222  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     496838.327   ± 5385.399  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499181.156   ± 7138.819  ops/s
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
