# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-10T08:00:39Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 77.21K | ± 1.19K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.24K | ± 658.15 | ops/s | 1.1x slower |
| prometheusAdd | 62.10K | ± 536.48 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 55.41K | ± 2.29K | ops/s | 1.4x slower |
| simpleclientInc | 8.16K | ± 56.64 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 7.94K | ± 167.09 | ops/s | 9.7x slower |
| simpleclientAdd | 7.52K | ± 409.99 | ops/s | 10x slower |
| openTelemetryAdd | 1.70K | ± 123.54 | ops/s | 45x slower |
| openTelemetryInc | 1.70K | ± 170.65 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.67K | ± 82.54 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.79K | ± 2.00K | ops/s | **fastest** |
| simpleclient | 5.68K | ± 97.97 | ops/s | 1.2x slower |
| prometheusNative | 4.06K | ± 47.40 | ops/s | 1.7x slower |
| openTelemetryClassic | 759.15 | ± 30.70 | ops/s | 8.9x slower |
| openTelemetryExponential | 654.02 | ± 6.65 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 679.79K | ± 6.08K | ops/s | **fastest** |
| prometheusWriteToByteArray | 668.53K | ± 10.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 647.01K | ± 4.03K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 627.55K | ± 5.63K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55410.375   ± 2290.717  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1701.227    ± 123.536  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1696.093    ± 170.646  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1671.712     ± 82.541  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62098.749    ± 536.479  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77207.690   ± 1187.575  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67240.911    ± 658.155  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7515.938    ± 409.991  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8159.983     ± 56.640  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7937.268    ± 167.090  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        759.155     ± 30.698  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        654.021      ± 6.650  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6791.173   ± 2004.399  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4060.644     ± 47.405  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5675.017     ± 97.969  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     627545.228   ± 5630.916  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     647011.385   ± 4032.807  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     668526.111  ± 10673.981  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     679790.402   ± 6079.701  ops/s
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
