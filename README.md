# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-01T06:30:25Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 62.74K | ± 2.60K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.04K | ± 198.32 | ops/s | 1.1x slower |
| prometheusAdd | 51.21K | ± 554.69 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 50.05K | ± 1.16K | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 181.75 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.57K | ± 54.78 | ops/s | 9.5x slower |
| simpleclientAdd | 6.18K | ± 248.45 | ops/s | 10x slower |
| openTelemetryInc | 1.40K | ± 266.13 | ops/s | 45x slower |
| openTelemetryAdd | 1.26K | ± 71.24 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.23K | ± 52.26 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.85K | ± 1.04K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 46.93 | ops/s | 1.3x slower |
| prometheusNative | 3.27K | ± 85.94 | ops/s | 1.8x slower |
| openTelemetryClassic | 663.79 | ± 2.43 | ops/s | 8.8x slower |
| openTelemetryExponential | 567.73 | ± 25.03 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.93K | ± 2.16K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.88K | ± 3.32K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.59K | ± 3.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.21K | ± 5.34K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50048.628   ± 1160.273  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1262.432     ± 71.245  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1399.967    ± 266.131  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1233.186     ± 52.260  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51206.476    ± 554.690  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      62738.191   ± 2599.384  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57042.463    ± 198.323  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6181.233    ± 248.451  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6593.426    ± 181.752  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6572.501     ± 54.776  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        663.787      ± 2.426  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.732     ± 25.029  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5852.430   ± 1043.636  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3265.162     ± 85.940  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4457.505     ± 46.932  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470205.947   ± 5341.291  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480591.827   ± 3298.308  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484884.019   ± 3321.109  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491933.475   ± 2160.698  ops/s
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
