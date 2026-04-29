# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-29T06:32:47Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 77.43K | ± 469.93 | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.37K | ± 591.59 | ops/s | 1.1x slower |
| prometheusAdd | 63.02K | ± 756.37 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 55.37K | ± 2.74K | ops/s | 1.4x slower |
| simpleclientInc | 7.93K | ± 135.74 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 7.90K | ± 331.98 | ops/s | 9.8x slower |
| simpleclientAdd | 7.56K | ± 291.44 | ops/s | 10x slower |
| openTelemetryAdd | 1.86K | ± 108.08 | ops/s | 42x slower |
| openTelemetryInc | 1.77K | ± 167.42 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.73K | ± 105.23 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.89K | ± 2.17K | ops/s | **fastest** |
| simpleclient | 5.61K | ± 56.37 | ops/s | 1.2x slower |
| prometheusNative | 4.12K | ± 22.18 | ops/s | 1.7x slower |
| openTelemetryClassic | 817.95 | ± 18.75 | ops/s | 8.4x slower |
| openTelemetryExponential | 677.03 | ± 15.72 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 677.52K | ± 9.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 665.87K | ± 4.15K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 645.24K | ± 5.84K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 620.84K | ± 17.72K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55369.284   ± 2735.177  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1858.468    ± 108.076  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1774.398    ± 167.419  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1727.706    ± 105.228  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63021.450    ± 756.367  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77429.206    ± 469.929  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67371.906    ± 591.591  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7560.239    ± 291.435  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7934.087    ± 135.738  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7902.826    ± 331.984  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        817.952     ± 18.751  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        677.027     ± 15.718  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6890.359   ± 2172.886  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4116.691     ± 22.183  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5614.522     ± 56.375  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     620840.592  ± 17722.761  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     645237.513   ± 5844.687  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     665874.631   ± 4154.126  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     677515.554   ± 9895.779  ops/s
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
