# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-16T08:11:59Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 79.13K | ± 249.99 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.45K | ± 1.30K | ops/s | 1.2x slower |
| prometheusAdd | 61.19K | ± 2.13K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.60K | ± 7.36K | ops/s | 1.7x slower |
| simpleclientInc | 7.82K | ± 214.13 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 7.80K | ± 182.48 | ops/s | 10x slower |
| simpleclientAdd | 7.79K | ± 190.93 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.94K | ± 67.91 | ops/s | 41x slower |
| openTelemetryInc | 1.90K | ± 122.79 | ops/s | 42x slower |
| openTelemetryAdd | 1.73K | ± 41.28 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.55K | ± 1.44K | ops/s | **fastest** |
| simpleclient | 5.60K | ± 93.85 | ops/s | 1.3x slower |
| prometheusNative | 3.88K | ± 320.37 | ops/s | 1.9x slower |
| openTelemetryClassic | 789.19 | ± 35.84 | ops/s | 9.6x slower |
| openTelemetryExponential | 669.08 | ± 38.11 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 681.17K | ± 6.44K | ops/s | **fastest** |
| prometheusWriteToByteArray | 671.37K | ± 2.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 650.15K | ± 4.63K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 635.58K | ± 2.49K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47597.729   ± 7355.946  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1733.359     ± 41.279  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1902.771    ± 122.791  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1935.561     ± 67.907  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61188.825   ± 2131.257  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      79125.743    ± 249.988  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66445.004   ± 1302.148  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7791.679    ± 190.929  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7822.035    ± 214.127  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7802.256    ± 182.484  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        789.195     ± 35.844  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        669.078     ± 38.108  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7554.526   ± 1439.348  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3882.198    ± 320.372  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5596.085     ± 93.850  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     635584.138   ± 2489.155  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     650151.277   ± 4628.911  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     671373.297   ± 2295.900  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     681169.066   ± 6444.991  ops/s
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
