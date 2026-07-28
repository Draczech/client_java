# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-28T06:07:26Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.65K | ± 3.76K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.89K | ± 498.09 | ops/s | 1.1x slower |
| prometheusAdd | 51.56K | ± 188.45 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.12K | ± 174.82 | ops/s | 1.4x slower |
| simpleclientInc | 6.42K | ± 133.37 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.28K | ± 93.21 | ops/s | 10x slower |
| simpleclientAdd | 6.15K | ± 266.81 | ops/s | 10x slower |
| openTelemetryAdd | 1.59K | ± 309.37 | ops/s | 40x slower |
| openTelemetryInc | 1.45K | ± 153.18 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.25K | ± 124.87 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.86K | ± 1.12K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 29.38 | ops/s | 1.3x slower |
| prometheusNative | 3.12K | ± 334.85 | ops/s | 1.9x slower |
| openTelemetryClassic | 678.08 | ± 23.53 | ops/s | 8.6x slower |
| openTelemetryExponential | 560.39 | ± 17.74 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.12K | ± 5.71K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.33K | ± 9.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.64K | ± 4.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.74K | ± 5.05K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47118.002    ± 174.821  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1589.052    ± 309.371  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1446.608    ± 153.184  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1254.499    ± 124.871  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51558.712    ± 188.453  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63648.823   ± 3756.765  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56889.927    ± 498.091  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6149.466    ± 266.812  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6416.694    ± 133.367  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6279.904     ± 93.206  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        678.082     ± 23.530  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.390     ± 17.741  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5863.754   ± 1115.090  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3123.777    ± 334.847  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.335     ± 29.377  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470742.710   ± 5046.595  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473642.175   ± 4119.806  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482330.657   ± 9293.156  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486121.642   ± 5707.434  ops/s
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
