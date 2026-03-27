# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-27T05:40:17Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.42K | ± 395.42 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 369.56 | ops/s | 1.2x slower |
| prometheusAdd | 50.80K | ± 1.01K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.53K | ± 710.87 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.45K | ± 132.06 | ops/s | 10x slower |
| simpleclientInc | 6.38K | ± 12.87 | ops/s | 10x slower |
| simpleclientAdd | 6.35K | ± 209.39 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.41K | ± 191.76 | ops/s | 47x slower |
| openTelemetryInc | 1.28K | ± 31.25 | ops/s | 52x slower |
| openTelemetryAdd | 1.28K | ± 18.62 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.43K | ± 1.30K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 49.48 | ops/s | 1.2x slower |
| prometheusNative | 3.00K | ± 388.47 | ops/s | 1.8x slower |
| openTelemetryClassic | 689.02 | ± 42.70 | ops/s | 7.9x slower |
| openTelemetryExponential | 583.79 | ± 31.93 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 482.35K | ± 7.83K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.22K | ± 4.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.80K | ± 4.64K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.20K | ± 3.43K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49529.553    ± 710.872  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1279.341     ± 18.619  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1283.428     ± 31.246  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1412.405    ± 191.762  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50799.104   ± 1009.524  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66419.322    ± 395.420  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56827.527    ± 369.559  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6345.207    ± 209.392  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6380.706     ± 12.868  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6449.097    ± 132.056  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        689.020     ± 42.699  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.786     ± 31.925  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5431.057   ± 1299.768  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3000.519    ± 388.466  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4446.451     ± 49.483  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470200.299   ± 3428.877  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476803.849   ± 4643.102  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480217.671   ± 4585.160  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482353.676   ± 7828.921  ops/s
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
