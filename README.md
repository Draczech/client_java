# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-27T08:31:20Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.52K | ± 1.68K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.10K | ± 1.37K | ops/s | 1.2x slower |
| prometheusAdd | 51.17K | ± 574.01 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.41K | ± 1.45K | ops/s | 1.4x slower |
| simpleclientInc | 6.58K | ± 165.01 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.38K | ± 192.51 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 230.06 | ops/s | 11x slower |
| openTelemetryAdd | 1.43K | ± 248.51 | ops/s | 46x slower |
| openTelemetryInc | 1.40K | ± 221.89 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.24K | ± 8.04 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.16K | ± 309.47 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 53.07 | ops/s | 1.2x slower |
| prometheusNative | 2.79K | ± 290.69 | ops/s | 1.8x slower |
| openTelemetryClassic | 699.00 | ± 47.50 | ops/s | 7.4x slower |
| openTelemetryExponential | 579.21 | ± 33.22 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.82K | ± 2.23K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.72K | ± 1.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.18K | ± 6.09K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 480.62K | ± 4.83K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48411.496   ± 1450.526  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1428.316    ± 248.512  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1404.278    ± 221.894  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1236.396      ± 8.041  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51165.737    ± 574.012  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65518.267   ± 1677.022  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56100.997   ± 1367.181  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6162.569    ± 230.064  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6581.904    ± 165.006  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6384.558    ± 192.514  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        698.998     ± 47.505  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        579.211     ± 33.218  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5155.034    ± 309.472  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2789.703    ± 290.694  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4455.285     ± 53.070  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     480624.871   ± 4828.650  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483176.358   ± 6085.571  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490716.717   ± 1442.600  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493824.016   ± 2230.636  ops/s
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
