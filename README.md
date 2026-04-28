# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-28T06:36:29Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.04K | ± 409.42 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.44K | ± 101.63 | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 379.43 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.79K | ± 525.71 | ops/s | 1.4x slower |
| simpleclientInc | 6.54K | ± 126.50 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.21K | ± 37.63 | ops/s | 11x slower |
| simpleclientAdd | 6.16K | ± 236.34 | ops/s | 11x slower |
| openTelemetryAdd | 1.45K | ± 196.00 | ops/s | 46x slower |
| openTelemetryInc | 1.37K | ± 196.73 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.18K | ± 36.84 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 888.52 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 47.31 | ops/s | 1.2x slower |
| prometheusNative | 3.02K | ± 343.91 | ops/s | 1.7x slower |
| openTelemetryClassic | 670.98 | ± 19.38 | ops/s | 7.8x slower |
| openTelemetryExponential | 598.99 | ± 19.41 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 476.05K | ± 4.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 474.30K | ± 6.21K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.06K | ± 7.16K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 453.09K | ± 13.39K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47790.007    ± 525.712  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1450.452    ± 196.003  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1368.557    ± 196.731  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1175.074     ± 36.836  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51427.974    ± 379.431  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66044.981    ± 409.423  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56438.372    ± 101.634  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6162.741    ± 236.345  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6542.072    ± 126.501  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6207.062     ± 37.629  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        670.984     ± 19.379  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        598.987     ± 19.407  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5251.786    ± 888.520  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3021.583    ± 343.914  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4465.262     ± 47.309  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     453089.619  ± 13392.013  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471056.309   ± 7158.624  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     474298.054   ± 6212.625  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     476049.144   ± 4165.363  ops/s
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
