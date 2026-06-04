# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-04T07:42:34Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.29K | ± 602.46 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.18K | ± 447.36 | ops/s | 1.2x slower |
| prometheusAdd | 48.18K | ± 261.82 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.28K | ± 601.57 | ops/s | 1.4x slower |
| simpleclientInc | 6.13K | ± 150.06 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.06K | ± 379.93 | ops/s | 10.0x slower |
| simpleclientAdd | 5.83K | ± 289.10 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.53K | ± 76.28 | ops/s | 39x slower |
| openTelemetryInc | 1.40K | ± 37.17 | ops/s | 43x slower |
| openTelemetryAdd | 1.33K | ± 31.00 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.48K | ± 940.23 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 39.42 | ops/s | 1.0x slower |
| prometheusNative | 3.12K | ± 68.35 | ops/s | 1.4x slower |
| openTelemetryClassic | 599.69 | ± 24.83 | ops/s | 7.5x slower |
| openTelemetryExponential | 532.70 | ± 30.69 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 550.17K | ± 9.34K | ops/s | **fastest** |
| prometheusWriteToByteArray | 540.75K | ± 2.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 531.25K | ± 4.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 516.07K | ± 4.87K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44283.829    ± 601.570  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1327.134     ± 31.000  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1396.199     ± 37.167  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1534.572     ± 76.280  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48183.859    ± 261.817  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60294.907    ± 602.456  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52177.050    ± 447.355  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5833.786    ± 289.099  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6128.022    ± 150.058  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6059.155    ± 379.934  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        599.695     ± 24.830  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        532.703     ± 30.686  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4480.124    ± 940.230  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3124.516     ± 68.348  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4372.580     ± 39.422  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     516068.314   ± 4872.213  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     531251.831   ± 4808.530  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     540750.412   ± 2820.110  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     550172.725   ± 9341.223  ops/s
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
