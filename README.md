# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-12T05:09:33Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.04K | ± 1.24K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.17K | ± 1.35K | ops/s | 1.2x slower |
| prometheusAdd | 51.30K | ± 294.29 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.35K | ± 1.47K | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 199.69 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 191.19 | ops/s | 10x slower |
| simpleclientAdd | 6.12K | ± 210.94 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.32K | ± 209.41 | ops/s | 49x slower |
| openTelemetryAdd | 1.30K | ± 28.94 | ops/s | 50x slower |
| openTelemetryInc | 1.23K | ± 42.45 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.76K | ± 1.36K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 44.80 | ops/s | 1.3x slower |
| prometheusNative | 2.84K | ± 314.92 | ops/s | 2.0x slower |
| openTelemetryClassic | 707.33 | ± 18.37 | ops/s | 8.1x slower |
| openTelemetryExponential | 570.06 | ± 33.32 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 488.02K | ± 5.37K | ops/s | **fastest** |
| prometheusWriteToNull | 482.99K | ± 7.21K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.81K | ± 4.16K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.64K | ± 3.80K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49345.196   ± 1468.748  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1303.543     ± 28.942  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1226.236     ± 42.447  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1315.558    ± 209.411  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51302.562    ± 294.289  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65035.654   ± 1239.375  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56169.188   ± 1350.647  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6120.243    ± 210.944  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6589.784    ± 199.693  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6484.465    ± 191.190  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        707.325     ± 18.373  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        570.061     ± 33.322  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5763.136   ± 1355.921  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2839.036    ± 314.925  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4451.277     ± 44.803  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472642.685   ± 3796.718  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478814.712   ± 4157.861  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488016.930   ± 5367.170  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482992.099   ± 7213.184  ops/s
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
