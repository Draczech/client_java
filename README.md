# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-25T04:04:53Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 78.46K | ± 1.02K | ops/s | **fastest** |
| prometheusNoLabelsInc | 64.59K | ± 3.29K | ops/s | 1.2x slower |
| prometheusAdd | 61.63K | ± 651.31 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 57.48K | ± 376.44 | ops/s | 1.4x slower |
| simpleclientInc | 7.88K | ± 286.54 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 7.73K | ± 252.23 | ops/s | 10x slower |
| simpleclientAdd | 7.39K | ± 473.92 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.87K | ± 32.09 | ops/s | 42x slower |
| openTelemetryAdd | 1.69K | ± 134.14 | ops/s | 46x slower |
| openTelemetryInc | 1.66K | ± 21.28 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.83K | ± 2.29K | ops/s | **fastest** |
| simpleclient | 5.84K | ± 95.89 | ops/s | 1.3x slower |
| prometheusNative | 3.73K | ± 299.00 | ops/s | 2.1x slower |
| openTelemetryClassic | 756.50 | ± 25.02 | ops/s | 10x slower |
| openTelemetryExponential | 646.00 | ± 10.83 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 668.51K | ± 5.24K | ops/s | **fastest** |
| prometheusWriteToByteArray | 657.44K | ± 7.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 637.76K | ± 8.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 627.05K | ± 3.82K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57476.035    ± 376.442  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1688.188    ± 134.135  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1655.205     ± 21.278  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1870.784     ± 32.086  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61630.881    ± 651.308  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      78455.132   ± 1022.785  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      64589.461   ± 3285.805  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7391.519    ± 473.919  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7876.072    ± 286.536  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7734.994    ± 252.226  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        756.502     ± 25.025  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        646.004     ± 10.833  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7828.381   ± 2291.485  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3731.056    ± 298.996  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5836.922     ± 95.891  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     627045.864   ± 3822.683  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     637756.211   ± 8466.005  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     657439.242   ± 7257.393  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     668508.055   ± 5240.344  ops/s
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
