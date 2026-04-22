# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-22T05:52:37Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 56.55K | ± 5.28K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.85K | ± 92.57 | ops/s | 1.1x slower |
| prometheusAdd | 48.13K | ± 502.25 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.30K | ± 422.33 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.23K | ± 25.06 | ops/s | 9.1x slower |
| simpleclientInc | 6.08K | ± 189.18 | ops/s | 9.3x slower |
| simpleclientAdd | 5.95K | ± 177.95 | ops/s | 9.5x slower |
| openTelemetryInc | 1.39K | ± 16.49 | ops/s | 41x slower |
| openTelemetryAdd | 1.37K | ± 44.31 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.34K | ± 64.55 | ops/s | 42x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.40K | ± 1.59K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 19.47 | ops/s | 1.2x slower |
| prometheusNative | 2.96K | ± 247.70 | ops/s | 1.8x slower |
| openTelemetryClassic | 620.48 | ± 31.22 | ops/s | 8.7x slower |
| openTelemetryExponential | 516.25 | ± 25.64 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.61K | ± 5.00K | ops/s | **fastest** |
| prometheusWriteToByteArray | 521.85K | ± 7.17K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 504.64K | ± 9.14K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 488.20K | ± 10.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44296.690    ± 422.329  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1366.350     ± 44.314  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1394.520     ± 16.489  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1336.849     ± 64.555  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48132.443    ± 502.252  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      56551.568   ± 5279.074  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51845.215     ± 92.575  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5952.642    ± 177.951  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6083.281    ± 189.181  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6231.701     ± 25.060  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        620.479     ± 31.222  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        516.246     ± 25.640  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5398.747   ± 1592.058  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2960.615    ± 247.698  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4510.396     ± 19.469  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488200.037  ± 10503.692  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     504636.035   ± 9136.517  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     521847.002   ± 7174.618  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532605.981   ± 5004.634  ops/s
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
