# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-21T08:36:50Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusAdd | 36.32K | ± 566.56 | ops/s | **fastest** |
| prometheusInc | 35.40K | ± 347.58 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 35.35K | ± 1.27K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 33.72K | ± 1.60K | ops/s | 1.1x slower |
| simpleclientInc | 9.02K | ± 222.72 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 9.01K | ± 282.12 | ops/s | 4.0x slower |
| simpleclientAdd | 8.75K | ± 169.64 | ops/s | 4.2x slower |
| openTelemetryInc | 882.45 | ± 22.09 | ops/s | 41x slower |
| openTelemetryAdd | 867.03 | ± 51.65 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 846.12 | ± 29.98 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.80K | ± 175.77 | ops/s | **fastest** |
| prometheusClassic | 2.48K | ± 584.41 | ops/s | 2.3x slower |
| prometheusNative | 2.25K | ± 161.48 | ops/s | 2.6x slower |
| openTelemetryClassic | 379.88 | ± 22.35 | ops/s | 15x slower |
| openTelemetryExponential | 355.44 | ± 20.52 | ops/s | 16x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 350.61K | ± 7.56K | ops/s | **fastest** |
| prometheusWriteToByteArray | 330.59K | ± 6.51K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 317.85K | ± 5.85K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 315.43K | ± 4.24K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      33718.017   ± 1596.442  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15        867.030     ± 51.648  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15        882.452     ± 22.088  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15        846.125     ± 29.975  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      36315.129    ± 566.561  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      35395.958    ± 347.578  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      35353.203   ± 1272.231  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       8749.659    ± 169.643  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       9016.798    ± 222.719  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       9005.442    ± 282.123  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        379.881     ± 22.351  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        355.437     ± 20.525  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2476.181    ± 584.412  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2247.355    ± 161.482  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5803.523    ± 175.771  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     315434.566   ± 4237.899  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     317853.929   ± 5850.972  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     330593.009   ± 6505.884  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     350612.534   ± 7558.721  ops/s
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
