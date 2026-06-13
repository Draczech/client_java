# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-13T07:22:14Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.57K | ± 16.35 | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.75K | ± 1.08K | ops/s | 1.1x slower |
| codahaleIncNoLabels | 29.12K | ± 713.87 | ops/s | 1.1x slower |
| prometheusAdd | 28.48K | ± 39.24 | ops/s | 1.1x slower |
| simpleclientInc | 6.90K | ± 134.75 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.71K | ± 323.07 | ops/s | 4.7x slower |
| simpleclientAdd | 6.43K | ± 217.46 | ops/s | 4.9x slower |
| openTelemetryInc | 1.40K | ± 40.36 | ops/s | 23x slower |
| openTelemetryIncNoLabels | 1.36K | ± 126.75 | ops/s | 23x slower |
| openTelemetryAdd | 1.31K | ± 66.78 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.45K | ± 84.80 | ops/s | **fastest** |
| prometheusClassic | 2.68K | ± 422.79 | ops/s | 1.7x slower |
| prometheusNative | 2.17K | ± 121.51 | ops/s | 2.0x slower |
| openTelemetryClassic | 523.71 | ± 22.47 | ops/s | 8.5x slower |
| openTelemetryExponential | 422.20 | ± 8.75 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 315.54K | ± 1.11K | ops/s | **fastest** |
| prometheusWriteToByteArray | 313.81K | ± 2.96K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 295.35K | ± 2.21K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 295.05K | ± 2.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29121.843    ± 713.866  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1307.032     ± 66.779  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1401.069     ± 40.357  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1362.289    ± 126.750  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28482.632     ± 39.237  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31568.301     ± 16.348  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29750.152   ± 1076.227  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6430.030    ± 217.461  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6900.249    ± 134.753  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6709.927    ± 323.075  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        523.712     ± 22.466  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        422.196      ± 8.746  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2683.903    ± 422.795  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2171.763    ± 121.511  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4450.413     ± 84.803  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     295054.689   ± 2286.712  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     295351.294   ± 2211.955  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     313811.339   ± 2956.844  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     315540.539   ± 1110.791  ops/s
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
