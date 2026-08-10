# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-10T04:57:47Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.50K | ± 335.64 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.47K | ± 460.63 | ops/s | 1.2x slower |
| prometheusAdd | 48.98K | ± 560.12 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.42K | ± 497.34 | ops/s | 1.3x slower |
| simpleclientInc | 6.15K | ± 96.85 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.09K | ± 214.35 | ops/s | 9.8x slower |
| simpleclientAdd | 6.01K | ± 237.19 | ops/s | 9.9x slower |
| openTelemetryInc | 1.54K | ± 38.99 | ops/s | 39x slower |
| openTelemetryAdd | 1.38K | ± 101.51 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.32K | ± 132.19 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.61K | ± 2.42K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 91.56 | ops/s | 1.7x slower |
| prometheusNative | 3.01K | ± 177.76 | ops/s | 2.5x slower |
| openTelemetryClassic | 593.32 | ± 8.41 | ops/s | 13x slower |
| openTelemetryExponential | 506.16 | ± 5.18 | ops/s | 15x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 530.72K | ± 12.61K | ops/s | **fastest** |
| openMetricsWriteToNull | 512.38K | ± 6.68K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 505.26K | ± 15.43K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 495.08K | ± 9.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44418.532    ± 497.343  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1383.739    ± 101.515  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1536.952     ± 38.986  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1323.011    ± 132.189  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48982.885    ± 560.116  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59502.432    ± 335.639  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51474.578    ± 460.635  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6009.260    ± 237.189  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6148.813     ± 96.855  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6093.273    ± 214.347  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        593.320      ± 8.413  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        506.160      ± 5.184  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7612.980   ± 2415.504  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3010.262    ± 177.763  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4454.804     ± 91.557  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     495082.585   ± 9725.728  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512383.982   ± 6683.698  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     505262.435  ± 15429.694  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     530718.076  ± 12612.090  ops/s
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
