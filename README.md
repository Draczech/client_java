# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-06T05:50:06Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.47K | ± 1.54K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.72K | ± 324.20 | ops/s | 1.1x slower |
| prometheusAdd | 51.40K | ± 275.62 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 42.58K | ± 7.60K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 6.60K | ± 17.77 | ops/s | 9.8x slower |
| simpleclientInc | 6.54K | ± 167.80 | ops/s | 9.9x slower |
| simpleclientAdd | 6.36K | ± 195.04 | ops/s | 10x slower |
| openTelemetryAdd | 1.58K | ± 241.31 | ops/s | 41x slower |
| openTelemetryInc | 1.26K | ± 6.28 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.17K | ± 34.19 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.73K | ± 670.76 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 83.08 | ops/s | 1.1x slower |
| prometheusNative | 2.90K | ± 319.16 | ops/s | 1.6x slower |
| openTelemetryClassic | 676.58 | ± 30.31 | ops/s | 7.0x slower |
| openTelemetryExponential | 562.44 | ± 14.60 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.40K | ± 5.95K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.05K | ± 4.05K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 484.26K | ± 4.63K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.79K | ± 4.24K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42582.754   ± 7600.266  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1583.723    ± 241.310  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1261.936      ± 6.276  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1166.762     ± 34.187  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51400.348    ± 275.616  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64467.718   ± 1543.409  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56724.635    ± 324.202  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6361.955    ± 195.036  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6541.647    ± 167.798  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6603.776     ± 17.767  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        676.581     ± 30.310  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.438     ± 14.604  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4726.232    ± 670.758  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2904.548    ± 319.164  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4434.266     ± 83.082  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478786.852   ± 4238.027  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484256.290   ± 4631.082  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486053.876   ± 4046.514  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488395.624   ± 5946.183  ops/s
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
