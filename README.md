# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-12T05:53:21Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.09K | ± 1.66K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.33K | ± 163.62 | ops/s | 1.1x slower |
| prometheusAdd | 51.17K | ± 158.70 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 42.88K | ± 6.90K | ops/s | 1.5x slower |
| simpleclientInc | 6.60K | ± 181.62 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.41K | ± 179.11 | ops/s | 10x slower |
| simpleclientAdd | 5.95K | ± 106.72 | ops/s | 11x slower |
| openTelemetryAdd | 1.38K | ± 36.71 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.30K | ± 119.14 | ops/s | 50x slower |
| openTelemetryInc | 1.29K | ± 8.75 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.42K | ± 97.79 | ops/s | **fastest** |
| prometheusClassic | 4.36K | ± 353.97 | ops/s | 1.0x slower |
| prometheusNative | 2.66K | ± 118.41 | ops/s | 1.7x slower |
| openTelemetryClassic | 688.81 | ± 20.95 | ops/s | 6.4x slower |
| openTelemetryExponential | 531.94 | ± 19.43 | ops/s | 8.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.93K | ± 1.76K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.48K | ± 2.76K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.56K | ± 3.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 472.73K | ± 5.40K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42876.212   ± 6899.757  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1375.616     ± 36.713  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1285.723      ± 8.754  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1298.736    ± 119.136  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51171.465    ± 158.695  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65090.992   ± 1656.981  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57331.735    ± 163.620  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5952.903    ± 106.722  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6599.016    ± 181.624  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6412.044    ± 179.107  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        688.808     ± 20.951  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        531.936     ± 19.429  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4363.358    ± 353.972  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2657.327    ± 118.414  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.791     ± 97.790  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482561.525   ± 3593.408  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     472725.176   ± 5395.537  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486483.825   ± 2759.518  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489926.930   ± 1763.201  ops/s
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
