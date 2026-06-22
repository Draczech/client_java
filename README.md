# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-22T08:24:58Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.21K | ± 347.48 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.78K | ± 599.67 | ops/s | 1.2x slower |
| prometheusAdd | 51.50K | ± 182.31 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.90K | ± 1.02K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.58K | ± 53.30 | ops/s | 10x slower |
| simpleclientInc | 6.49K | ± 152.68 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 206.13 | ops/s | 11x slower |
| openTelemetryInc | 1.51K | ± 239.68 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.28K | ± 118.40 | ops/s | 52x slower |
| openTelemetryAdd | 1.17K | ± 34.69 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.84K | ± 1.65K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 13.87 | ops/s | 1.1x slower |
| prometheusNative | 2.94K | ± 129.92 | ops/s | 1.6x slower |
| openTelemetryClassic | 723.19 | ± 7.56 | ops/s | 6.7x slower |
| openTelemetryExponential | 573.46 | ± 23.59 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 480.05K | ± 9.35K | ops/s | **fastest** |
| openMetricsWriteToNull | 479.25K | ± 3.71K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 473.82K | ± 4.90K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.62K | ± 7.08K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48900.975   ± 1015.019  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1169.209     ± 34.690  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1510.848    ± 239.675  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1281.889    ± 118.399  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51498.634    ± 182.306  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66211.644    ± 347.484  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56781.165    ± 599.672  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6187.932    ± 206.134  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6488.208    ± 152.682  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6578.510     ± 53.305  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        723.190      ± 7.560  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        573.462     ± 23.591  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4844.661   ± 1647.669  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2940.814    ± 129.918  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4378.734     ± 13.866  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469619.610   ± 7075.334  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479251.028   ± 3705.448  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     473817.609   ± 4902.057  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     480051.064   ± 9350.286  ops/s
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
