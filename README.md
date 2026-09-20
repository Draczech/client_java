# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-20T08:28:01Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 54.91K | ± 1.51K | ops/s | **fastest** |
| prometheusNoLabelsInc | 48.68K | ± 1.44K | ops/s | 1.1x slower |
| prometheusAdd | 43.44K | ± 444.22 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 41.55K | ± 1.71K | ops/s | 1.3x slower |
| simpleclientInc | 5.64K | ± 155.69 | ops/s | 9.7x slower |
| simpleclientAdd | 5.35K | ± 222.01 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.30K | ± 109.38 | ops/s | 10x slower |
| openTelemetryInc | 1.31K | ± 142.35 | ops/s | 42x slower |
| openTelemetryAdd | 1.25K | ± 90.82 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.24K | ± 90.07 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.02K | ± 898.57 | ops/s | **fastest** |
| simpleclient | 3.72K | ± 55.30 | ops/s | 1.3x slower |
| prometheusNative | 2.81K | ± 103.71 | ops/s | 1.8x slower |
| openTelemetryClassic | 588.59 | ± 43.30 | ops/s | 8.5x slower |
| openTelemetryExponential | 469.19 | ± 21.40 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 483.05K | ± 7.37K | ops/s | **fastest** |
| prometheusWriteToByteArray | 476.49K | ± 6.68K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.91K | ± 24.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 465.53K | ± 11.69K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      41549.971   ± 1706.872  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1248.225     ± 90.817  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1312.903    ± 142.347  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1238.805     ± 90.065  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      43442.596    ± 444.225  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      54912.911   ± 1509.419  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      48677.980   ± 1444.040  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5353.359    ± 222.006  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       5640.436    ± 155.695  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5304.688    ± 109.383  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        588.586     ± 43.304  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        469.187     ± 21.402  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5023.082    ± 898.566  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2811.605    ± 103.708  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       3723.626     ± 55.299  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473909.425  ± 24839.367  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     465528.484  ± 11689.936  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476493.329   ± 6682.326  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     483054.530   ± 7374.670  ops/s
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
