# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-09T07:08:55Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 31.37K | ± 291.00 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.60K | ± 182.99 | ops/s | 1.0x slower |
| prometheusInc | 30.42K | ± 220.20 | ops/s | 1.0x slower |
| prometheusAdd | 29.36K | ± 317.84 | ops/s | 1.1x slower |
| simpleclientInc | 7.53K | ± 110.29 | ops/s | 4.2x slower |
| simpleclientAdd | 7.43K | ± 119.88 | ops/s | 4.2x slower |
| simpleclientNoLabelsInc | 7.41K | ± 89.15 | ops/s | 4.2x slower |
| openTelemetryIncNoLabels | 1.37K | ± 112.15 | ops/s | 23x slower |
| openTelemetryAdd | 1.21K | ± 77.29 | ops/s | 26x slower |
| openTelemetryInc | 1.20K | ± 26.80 | ops/s | 26x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.74K | ± 127.71 | ops/s | **fastest** |
| prometheusClassic | 3.54K | ± 2.25K | ops/s | 1.3x slower |
| prometheusNative | 2.10K | ± 286.03 | ops/s | 2.3x slower |
| openTelemetryClassic | 403.89 | ± 16.44 | ops/s | 12x slower |
| openTelemetryExponential | 377.27 | ± 21.70 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 297.21K | ± 3.04K | ops/s | **fastest** |
| prometheusWriteToNull | 296.42K | ± 3.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 281.78K | ± 3.72K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 279.18K | ± 2.54K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      31372.953    ± 290.995  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1213.968     ± 77.288  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1198.691     ± 26.796  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1370.354    ± 112.152  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      29364.126    ± 317.838  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30415.603    ± 220.196  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30597.933    ± 182.992  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7431.182    ± 119.884  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7532.485    ± 110.288  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7414.107     ± 89.146  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        403.889     ± 16.443  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        377.273     ± 21.701  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3537.446   ± 2253.585  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2096.095    ± 286.030  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4737.142    ± 127.714  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     281782.949   ± 3724.964  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     279180.781   ± 2540.173  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     297206.105   ± 3039.680  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     296419.093   ± 3877.306  ops/s
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
