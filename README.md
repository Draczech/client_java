# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-11T05:26:14Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.59K | ± 40.86 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.84K | ± 816.71 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 30.02K | ± 1.80K | ops/s | 1.1x slower |
| prometheusAdd | 28.45K | ± 46.12 | ops/s | 1.1x slower |
| simpleclientInc | 7.00K | ± 28.91 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.82K | ± 192.86 | ops/s | 4.6x slower |
| simpleclientAdd | 6.48K | ± 245.01 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 1.43K | ± 107.07 | ops/s | 22x slower |
| openTelemetryInc | 1.37K | ± 110.42 | ops/s | 23x slower |
| openTelemetryAdd | 1.21K | ± 41.16 | ops/s | 26x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.48K | ± 23.36 | ops/s | **fastest** |
| prometheusClassic | 3.14K | ± 659.46 | ops/s | 1.4x slower |
| prometheusNative | 2.24K | ± 220.39 | ops/s | 2.0x slower |
| openTelemetryClassic | 493.19 | ± 16.59 | ops/s | 9.1x slower |
| openTelemetryExponential | 400.61 | ± 13.01 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 317.45K | ± 2.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 313.41K | ± 1.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 298.79K | ± 1.54K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 293.64K | ± 1.22K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30015.169   ± 1804.838  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1206.502     ± 41.156  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1366.563    ± 110.421  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1425.075    ± 107.070  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28453.188     ± 46.117  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31590.284     ± 40.858  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30839.869    ± 816.712  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6479.817    ± 245.014  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7003.503     ± 28.912  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6822.389    ± 192.861  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        493.191     ± 16.590  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        400.613     ± 13.012  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3143.661    ± 659.457  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2237.354    ± 220.392  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4478.578     ± 23.355  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     293643.030   ± 1223.805  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     298792.051   ± 1537.126  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     313406.371   ± 1430.096  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     317447.353   ± 2005.648  ops/s
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
