# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-05T06:08:18Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 26.32K | ± 384.97 | ops/s | **fastest** |
| prometheusNoLabelsInc | 26.24K | ± 466.51 | ops/s | 1.0x slower |
| prometheusInc | 25.75K | ± 30.78 | ops/s | 1.0x slower |
| prometheusAdd | 25.12K | ± 206.37 | ops/s | 1.0x slower |
| simpleclientAdd | 6.45K | ± 128.40 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 6.45K | ± 36.82 | ops/s | 4.1x slower |
| simpleclientInc | 6.45K | ± 26.83 | ops/s | 4.1x slower |
| openTelemetryIncNoLabels | 1.00K | ± 75.96 | ops/s | 26x slower |
| openTelemetryAdd | 992.24 | ± 105.31 | ops/s | 27x slower |
| openTelemetryInc | 957.18 | ± 70.44 | ops/s | 27x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.25K | ± 61.06 | ops/s | **fastest** |
| prometheusClassic | 2.78K | ± 307.30 | ops/s | 1.5x slower |
| prometheusNative | 1.81K | ± 293.33 | ops/s | 2.3x slower |
| openTelemetryClassic | 388.45 | ± 8.04 | ops/s | 11x slower |
| openTelemetryExponential | 334.34 | ± 6.37 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 289.13K | ± 1.72K | ops/s | **fastest** |
| prometheusWriteToNull | 288.64K | ± 852.39 | ops/s | 1.0x slower |
| openMetricsWriteToNull | 269.15K | ± 1.39K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 268.02K | ± 1.74K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      26318.168    ± 384.966  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15        992.243    ± 105.312  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15        957.177     ± 70.437  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1002.957     ± 75.964  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25123.525    ± 206.365  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      25745.145     ± 30.779  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26235.084    ± 466.511  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6453.475    ± 128.395  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6446.642     ± 26.825  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6450.355     ± 36.820  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        388.447      ± 8.044  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        334.336      ± 6.368  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2781.593    ± 307.301  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1812.623    ± 293.330  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4245.414     ± 61.061  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     268016.450   ± 1741.889  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     269150.629   ± 1389.333  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     289130.411   ± 1716.081  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     288641.042    ± 852.385  ops/s
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
