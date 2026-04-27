# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-27T06:13:49Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.11K | ± 1.08K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.19K | ± 118.73 | ops/s | 1.1x slower |
| prometheusAdd | 51.09K | ± 836.70 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.38K | ± 1.33K | ops/s | 1.3x slower |
| simpleclientInc | 6.64K | ± 97.83 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.60K | ± 15.80 | ops/s | 9.9x slower |
| simpleclientAdd | 6.11K | ± 287.02 | ops/s | 11x slower |
| openTelemetryInc | 1.39K | ± 112.55 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.31K | ± 194.23 | ops/s | 50x slower |
| openTelemetryAdd | 1.24K | ± 15.22 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.19K | ± 1.12K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 19.95 | ops/s | 1.2x slower |
| prometheusNative | 2.53K | ± 80.18 | ops/s | 2.1x slower |
| openTelemetryClassic | 726.26 | ± 29.31 | ops/s | 7.1x slower |
| openTelemetryExponential | 586.51 | ± 23.25 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 489.41K | ± 1.26K | ops/s | **fastest** |
| prometheusWriteToNull | 485.58K | ± 6.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.65K | ± 2.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.44K | ± 4.98K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50377.400   ± 1331.799  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1237.985     ± 15.219  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1389.182    ± 112.545  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1311.671    ± 194.234  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51085.418    ± 836.700  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65106.226   ± 1080.405  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57185.775    ± 118.726  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6108.099    ± 287.021  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6637.335     ± 97.827  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6604.427     ± 15.797  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        726.256     ± 29.311  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        586.507     ± 23.245  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5192.060   ± 1124.199  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2529.723     ± 80.181  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4415.181     ± 19.954  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478440.249   ± 4982.746  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482647.399   ± 2547.780  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489406.292   ± 1263.268  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485584.331   ± 6586.102  ops/s
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
