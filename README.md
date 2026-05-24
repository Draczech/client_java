# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-24T07:08:30Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.42K | ± 245.93 | ops/s | **fastest** |
| prometheusInc | 30.79K | ± 1.24K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.17K | ± 1.30K | ops/s | 1.1x slower |
| prometheusAdd | 27.37K | ± 1.77K | ops/s | 1.1x slower |
| simpleclientInc | 6.81K | ± 122.22 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.57K | ± 58.36 | ops/s | 4.8x slower |
| simpleclientAdd | 6.44K | ± 277.98 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 1.39K | ± 129.78 | ops/s | 23x slower |
| openTelemetryInc | 1.32K | ± 28.61 | ops/s | 24x slower |
| openTelemetryAdd | 1.29K | ± 47.93 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.42K | ± 70.03 | ops/s | **fastest** |
| prometheusClassic | 2.48K | ± 124.11 | ops/s | 1.8x slower |
| prometheusNative | 1.98K | ± 169.62 | ops/s | 2.2x slower |
| openTelemetryClassic | 484.38 | ± 31.10 | ops/s | 9.1x slower |
| openTelemetryExponential | 412.81 | ± 25.37 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 317.04K | ± 1.72K | ops/s | **fastest** |
| prometheusWriteToByteArray | 315.17K | ± 1.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 297.79K | ± 1.34K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 295.05K | ± 905.90 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29174.463   ± 1297.374  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1293.531     ± 47.929  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1318.936     ± 28.607  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1388.408    ± 129.783  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27369.717   ± 1768.788  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30785.352   ± 1242.679  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31418.843    ± 245.929  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6444.804    ± 277.977  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6812.889    ± 122.219  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6565.651     ± 58.365  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        484.376     ± 31.104  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        412.814     ± 25.367  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2481.400    ± 124.112  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1976.948    ± 169.623  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4424.699     ± 70.030  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     295054.903    ± 905.897  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     297793.673   ± 1342.454  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     315167.062   ± 1299.307  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     317038.232   ± 1720.479  ops/s
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
