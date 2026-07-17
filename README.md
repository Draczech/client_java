# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-17T06:07:01Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 28.67K | ± 440.34 | ops/s | **fastest** |
| codahaleIncNoLabels | 28.36K | ± 543.75 | ops/s | 1.0x slower |
| prometheusInc | 27.71K | ± 491.16 | ops/s | 1.0x slower |
| prometheusAdd | 26.97K | ± 188.94 | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 7.00K | ± 296.60 | ops/s | 4.1x slower |
| simpleclientAdd | 6.99K | ± 146.82 | ops/s | 4.1x slower |
| simpleclientInc | 6.95K | ± 45.93 | ops/s | 4.1x slower |
| openTelemetryInc | 1.10K | ± 45.87 | ops/s | 26x slower |
| openTelemetryIncNoLabels | 1.06K | ± 77.38 | ops/s | 27x slower |
| openTelemetryAdd | 1.02K | ± 13.01 | ops/s | 28x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.47K | ± 65.42 | ops/s | **fastest** |
| prometheusClassic | 3.81K | ± 1.71K | ops/s | 1.2x slower |
| prometheusNative | 2.13K | ± 167.03 | ops/s | 2.1x slower |
| openTelemetryClassic | 387.52 | ± 5.09 | ops/s | 12x slower |
| openTelemetryExponential | 329.23 | ± 12.48 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 298.32K | ± 2.63K | ops/s | **fastest** |
| prometheusWriteToByteArray | 295.42K | ± 2.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 281.16K | ± 1.78K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 279.64K | ± 1.98K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28358.677    ± 543.752  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1022.170     ± 13.010  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1100.318     ± 45.867  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1058.297     ± 77.381  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      26965.279    ± 188.939  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      27707.887    ± 491.159  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      28672.564    ± 440.336  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6994.440    ± 146.817  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6947.516     ± 45.929  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6999.164    ± 296.598  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        387.524      ± 5.091  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        329.228     ± 12.475  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3809.914   ± 1713.307  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2134.869    ± 167.033  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4471.470     ± 65.418  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     279642.769   ± 1975.874  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     281155.671   ± 1779.643  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     295423.258   ± 2786.232  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     298315.356   ± 2628.088  ops/s
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
