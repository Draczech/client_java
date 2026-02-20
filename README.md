# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-20T05:22:45Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.45K | ± 1.77K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.81K | ± 399.52 | ops/s | 1.2x slower |
| prometheusAdd | 51.60K | ± 265.89 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.73K | ± 503.06 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.69K | ± 39.05 | ops/s | 9.8x slower |
| simpleclientInc | 6.66K | ± 119.24 | ops/s | 9.8x slower |
| simpleclientAdd | 6.31K | ± 369.61 | ops/s | 10x slower |
| openTelemetryAdd | 1.41K | ± 219.98 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.30K | ± 181.49 | ops/s | 50x slower |
| openTelemetryInc | 1.23K | ± 43.30 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.70K | ± 448.78 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 31.40 | ops/s | 1.0x slower |
| prometheusNative | 3.08K | ± 236.78 | ops/s | 1.5x slower |
| openTelemetryClassic | 659.13 | ± 16.89 | ops/s | 7.1x slower |
| openTelemetryExponential | 533.18 | ± 8.43 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 487.39K | ± 6.78K | ops/s | **fastest** |
| openMetricsWriteToNull | 487.09K | ± 4.50K | ops/s | 1.0x slower |
| prometheusWriteToNull | 482.81K | ± 4.84K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 479.50K | ± 3.36K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47731.741    ± 503.060  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1410.432    ± 219.977  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1231.808     ± 43.296  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1298.604    ± 181.486  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51601.662    ± 265.888  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65450.691   ± 1771.727  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56811.199    ± 399.523  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6309.306    ± 369.606  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6662.842    ± 119.239  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6689.062     ± 39.046  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        659.131     ± 16.890  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        533.185      ± 8.434  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4698.202    ± 448.781  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3076.294    ± 236.780  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4549.694     ± 31.402  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479497.238   ± 3364.891  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487090.982   ± 4501.552  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487389.029   ± 6782.596  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482805.811   ± 4839.135  ops/s
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
