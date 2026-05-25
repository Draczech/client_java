# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-25T07:31:18Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.20K | ± 1.41K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.38K | ± 1.29K | ops/s | 1.2x slower |
| prometheusAdd | 51.64K | ± 169.71 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.09K | ± 968.42 | ops/s | 1.4x slower |
| simpleclientInc | 6.69K | ± 22.84 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.52K | ± 109.76 | ops/s | 10.0x slower |
| simpleclientAdd | 5.96K | ± 135.57 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.29K | ± 129.66 | ops/s | 51x slower |
| openTelemetryInc | 1.27K | ± 4.36 | ops/s | 51x slower |
| openTelemetryAdd | 1.26K | ± 9.44 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.04K | ± 759.46 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 59.49 | ops/s | 1.1x slower |
| prometheusNative | 3.01K | ± 203.69 | ops/s | 1.7x slower |
| openTelemetryClassic | 701.12 | ± 25.55 | ops/s | 7.2x slower |
| openTelemetryExponential | 563.36 | ± 29.12 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.44K | ± 1.76K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.07K | ± 2.03K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.43K | ± 1.43K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.64K | ± 19.35K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48093.263    ± 968.418  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1258.153      ± 9.437  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1270.395      ± 4.364  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1290.778    ± 129.660  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51641.890    ± 169.706  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65204.082   ± 1408.407  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56377.176   ± 1292.568  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5956.348    ± 135.568  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6690.347     ± 22.844  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6523.038    ± 109.763  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        701.119     ± 25.548  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        563.364     ± 29.121  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5036.442    ± 759.459  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3013.050    ± 203.690  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4443.604     ± 59.486  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466641.518  ± 19346.336  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485430.836   ± 1425.015  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490073.850   ± 2025.167  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493441.585   ± 1759.128  ops/s
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
