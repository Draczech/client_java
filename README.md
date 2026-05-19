# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-19T07:12:52Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.70K | ± 1.07K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.95K | ± 2.55K | ops/s | 1.2x slower |
| prometheusAdd | 51.70K | ± 333.70 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.73K | ± 458.23 | ops/s | 1.4x slower |
| simpleclientInc | 6.52K | ± 161.85 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.47K | ± 222.00 | ops/s | 10x slower |
| simpleclientAdd | 6.14K | ± 228.84 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.35K | ± 149.76 | ops/s | 48x slower |
| openTelemetryAdd | 1.29K | ± 105.87 | ops/s | 50x slower |
| openTelemetryInc | 1.25K | ± 8.79 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.85K | ± 1.13K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 62.80 | ops/s | 1.3x slower |
| prometheusNative | 3.00K | ± 265.15 | ops/s | 1.9x slower |
| openTelemetryClassic | 705.30 | ± 41.93 | ops/s | 8.3x slower |
| openTelemetryExponential | 562.92 | ± 42.73 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 482.61K | ± 3.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 471.90K | ± 5.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.66K | ± 5.96K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 461.82K | ± 4.75K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47725.436    ± 458.235  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1287.905    ± 105.870  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1251.137      ± 8.790  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1350.565    ± 149.756  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51695.117    ± 333.698  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64698.717   ± 1068.205  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54953.596   ± 2552.191  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6137.636    ± 228.838  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6518.930    ± 161.849  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6467.693    ± 222.002  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        705.304     ± 41.926  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.922     ± 42.735  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5847.517   ± 1132.719  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2999.293    ± 265.147  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4417.224     ± 62.798  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463664.997   ± 5955.400  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     461819.561   ± 4749.521  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     471904.563   ± 5115.634  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482614.191   ± 3356.443  ops/s
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
