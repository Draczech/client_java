# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-08T05:16:50Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 61.78K | ± 4.57K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.78K | ± 233.32 | ops/s | 1.1x slower |
| prometheusAdd | 51.33K | ± 518.66 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.94K | ± 520.72 | ops/s | 1.2x slower |
| simpleclientInc | 6.78K | ± 23.67 | ops/s | 9.1x slower |
| simpleclientNoLabelsInc | 6.47K | ± 181.44 | ops/s | 9.5x slower |
| simpleclientAdd | 6.18K | ± 230.46 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.29K | ± 41.60 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.23K | ± 41.58 | ops/s | 50x slower |
| openTelemetryInc | 1.21K | ± 68.93 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.73K | ± 683.03 | ops/s | **fastest** |
| simpleclient | 4.60K | ± 24.82 | ops/s | 1.0x slower |
| prometheusNative | 2.95K | ± 309.64 | ops/s | 1.6x slower |
| openTelemetryClassic | 697.65 | ± 70.43 | ops/s | 6.8x slower |
| openTelemetryExponential | 518.71 | ± 10.93 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.18K | ± 1.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 483.41K | ± 3.48K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 474.64K | ± 6.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.48K | ± 2.24K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49942.550    ± 520.715  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1294.317     ± 41.604  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1209.224     ± 68.935  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1228.472     ± 41.583  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51328.518    ± 518.661  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      61777.866   ± 4565.525  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56782.669    ± 233.322  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6180.958    ± 230.463  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6780.113     ± 23.668  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6473.833    ± 181.436  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        697.651     ± 70.430  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        518.707     ± 10.934  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4731.491    ± 683.034  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2952.512    ± 309.635  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4599.281     ± 24.819  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471476.317   ± 2243.064  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474639.450   ± 6876.339  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483414.039   ± 3479.719  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488176.523   ± 1892.126  ops/s
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
