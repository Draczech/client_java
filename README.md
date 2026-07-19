# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-19T06:14:11Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.92K | ± 2.55K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.08K | ± 968.97 | ops/s | 1.1x slower |
| prometheusAdd | 48.64K | ± 896.62 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.03K | ± 1.14K | ops/s | 1.3x slower |
| simpleclientInc | 6.18K | ± 136.83 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.14K | ± 230.26 | ops/s | 9.6x slower |
| simpleclientAdd | 5.80K | ± 250.89 | ops/s | 10x slower |
| openTelemetryInc | 1.39K | ± 138.74 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.35K | ± 117.15 | ops/s | 44x slower |
| openTelemetryAdd | 1.35K | ± 36.54 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.80K | ± 1.23K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 103.21 | ops/s | 1.3x slower |
| prometheusNative | 2.89K | ± 261.27 | ops/s | 2.0x slower |
| openTelemetryClassic | 572.51 | ± 11.30 | ops/s | 10x slower |
| openTelemetryExponential | 519.76 | ± 16.02 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 539.29K | ± 3.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 528.31K | ± 5.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 516.52K | ± 5.52K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.29K | ± 5.86K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44029.989   ± 1137.096  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1348.859     ± 36.539  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1389.320    ± 138.739  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1350.702    ± 117.149  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48644.602    ± 896.616  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58916.447   ± 2549.123  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52075.633    ± 968.970  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5800.794    ± 250.885  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6181.591    ± 136.830  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6141.720    ± 230.259  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        572.509     ± 11.301  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        519.757     ± 16.020  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5803.028   ± 1234.830  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2893.146    ± 261.275  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4407.946    ± 103.211  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509285.322   ± 5863.440  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     516523.837   ± 5517.753  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     528307.722   ± 5818.217  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     539286.189   ± 3013.390  ops/s
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
