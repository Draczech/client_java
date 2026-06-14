# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-14T07:39:40Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.16K | ± 3.77K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.31K | ± 353.90 | ops/s | 1.1x slower |
| prometheusAdd | 51.07K | ± 523.63 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.93K | ± 7.51K | ops/s | 1.4x slower |
| simpleclientInc | 6.53K | ± 152.83 | ops/s | 9.7x slower |
| simpleclientAdd | 6.48K | ± 10.96 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.47K | ± 204.22 | ops/s | 9.8x slower |
| openTelemetryInc | 1.29K | ± 37.12 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.26K | ± 95.20 | ops/s | 50x slower |
| openTelemetryAdd | 1.19K | ± 83.12 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.70K | ± 2.89K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 56.87 | ops/s | 1.5x slower |
| prometheusNative | 2.85K | ± 314.47 | ops/s | 2.3x slower |
| openTelemetryClassic | 667.73 | ± 36.48 | ops/s | 10x slower |
| openTelemetryExponential | 566.89 | ± 16.55 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.32K | ± 4.28K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.81K | ± 4.63K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 480.84K | ± 5.61K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.33K | ± 10.61K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43926.376   ± 7510.509  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1192.282     ± 83.118  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1285.801     ± 37.118  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1261.364     ± 95.203  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51074.884    ± 523.634  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63160.154   ± 3771.118  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57314.342    ± 353.905  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6479.962     ± 10.963  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6531.979    ± 152.828  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6471.138    ± 204.225  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        667.735     ± 36.476  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.893     ± 16.552  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6702.220   ± 2886.811  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2853.139    ± 314.473  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4440.571     ± 56.872  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     480835.974   ± 5611.283  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475329.666  ± 10611.233  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487813.087   ± 4629.943  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490321.371   ± 4277.631  ops/s
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
