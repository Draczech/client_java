# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-07T07:59:03Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.90K | ± 338.84 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.89K | ± 481.72 | ops/s | 1.2x slower |
| prometheusAdd | 51.28K | ± 492.37 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.39K | ± 2.12K | ops/s | 1.4x slower |
| simpleclientInc | 6.64K | ± 47.94 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.62K | ± 17.20 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 253.46 | ops/s | 11x slower |
| openTelemetryInc | 1.49K | ± 157.10 | ops/s | 45x slower |
| openTelemetryAdd | 1.46K | ± 219.13 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.41K | ± 145.90 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.18K | ± 946.66 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 55.87 | ops/s | 1.2x slower |
| prometheusNative | 3.17K | ± 102.76 | ops/s | 1.6x slower |
| openTelemetryClassic | 688.60 | ± 29.33 | ops/s | 7.5x slower |
| openTelemetryExponential | 575.16 | ± 25.12 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 467.20K | ± 6.39K | ops/s | **fastest** |
| openMetricsWriteToByteArray | 461.86K | ± 6.27K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 450.42K | ± 8.91K | ops/s | 1.0x slower |
| prometheusWriteToNull | 441.28K | ± 4.59K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48391.560   ± 2116.884  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1464.115    ± 219.133  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1490.707    ± 157.097  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1411.563    ± 145.901  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51277.502    ± 492.371  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66904.674    ± 338.837  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56885.495    ± 481.717  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6156.236    ± 253.461  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6644.480     ± 47.942  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6615.062     ± 17.198  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        688.603     ± 29.328  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.163     ± 25.118  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5176.482    ± 946.659  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3166.437    ± 102.762  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4412.394     ± 55.873  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     461859.589   ± 6269.627  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     467197.050   ± 6389.716  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     450419.656   ± 8909.645  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     441277.840   ± 4590.464  ops/s
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
