# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-25T07:11:46Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 56.68K | ± 2.50K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.49K | ± 424.62 | ops/s | 1.1x slower |
| prometheusAdd | 48.06K | ± 375.62 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.40K | ± 279.64 | ops/s | 1.3x slower |
| simpleclientInc | 6.15K | ± 104.63 | ops/s | 9.2x slower |
| simpleclientNoLabelsInc | 5.93K | ± 248.55 | ops/s | 9.6x slower |
| simpleclientAdd | 5.84K | ± 16.08 | ops/s | 9.7x slower |
| openTelemetryInc | 1.36K | ± 92.03 | ops/s | 42x slower |
| openTelemetryAdd | 1.30K | ± 122.39 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.20K | ± 87.64 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.58K | ± 38.60 | ops/s | **fastest** |
| prometheusClassic | 4.56K | ± 935.57 | ops/s | 1.0x slower |
| prometheusNative | 3.02K | ± 246.52 | ops/s | 1.5x slower |
| openTelemetryClassic | 586.86 | ± 13.89 | ops/s | 7.8x slower |
| openTelemetryExponential | 517.08 | ± 10.62 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.60K | ± 5.26K | ops/s | **fastest** |
| prometheusWriteToByteArray | 519.42K | ± 5.53K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 516.07K | ± 3.45K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 511.95K | ± 3.27K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44396.186    ± 279.639  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1301.636    ± 122.394  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1364.980     ± 92.027  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1200.900     ± 87.636  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48061.097    ± 375.618  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      56683.325   ± 2502.582  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51494.645    ± 424.621  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5839.334     ± 16.085  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6148.104    ± 104.632  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5932.331    ± 248.546  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        586.858     ± 13.888  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        517.077     ± 10.622  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4561.478    ± 935.571  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3019.636    ± 246.520  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4582.240     ± 38.596  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     511951.693   ± 3271.501  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     516065.809   ± 3451.312  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     519424.696   ± 5530.133  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532595.358   ± 5259.758  ops/s
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
