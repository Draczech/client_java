# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-03T08:27:32Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.42K | ± 606.45 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.98K | ± 447.57 | ops/s | 1.2x slower |
| prometheusAdd | 51.25K | ± 373.93 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.72K | ± 632.57 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.52K | ± 131.41 | ops/s | 10x slower |
| simpleclientInc | 6.40K | ± 151.60 | ops/s | 10x slower |
| simpleclientAdd | 6.16K | ± 263.49 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.34K | ± 252.60 | ops/s | 49x slower |
| openTelemetryAdd | 1.28K | ± 46.90 | ops/s | 52x slower |
| openTelemetryInc | 1.22K | ± 65.21 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.91K | ± 1.40K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 51.14 | ops/s | 1.3x slower |
| prometheusNative | 3.05K | ± 301.38 | ops/s | 1.9x slower |
| openTelemetryClassic | 648.45 | ± 11.35 | ops/s | 9.1x slower |
| openTelemetryExponential | 600.96 | ± 16.21 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 485.95K | ± 4.60K | ops/s | **fastest** |
| prometheusWriteToNull | 480.10K | ± 5.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.22K | ± 5.24K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 456.32K | ± 9.40K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50720.443    ± 632.574  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1278.880     ± 46.902  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1221.693     ± 65.208  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1342.220    ± 252.601  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51252.757    ± 373.932  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66416.859    ± 606.448  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56983.513    ± 447.568  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6163.945    ± 263.487  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6395.467    ± 151.597  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6524.310    ± 131.405  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        648.448     ± 11.354  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        600.956     ± 16.211  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5909.431   ± 1403.549  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3051.355    ± 301.381  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4437.804     ± 51.140  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     456319.534   ± 9395.074  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476216.001   ± 5236.448  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485952.303   ± 4595.201  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     480104.872   ± 5121.246  ops/s
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
