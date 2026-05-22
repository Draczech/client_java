# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-22T07:12:14Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.63K | ± 2.86K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.86K | ± 834.07 | ops/s | 1.1x slower |
| prometheusAdd | 48.92K | ± 660.38 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.62K | ± 610.51 | ops/s | 1.3x slower |
| simpleclientInc | 6.15K | ± 104.26 | ops/s | 9.5x slower |
| simpleclientAdd | 5.99K | ± 152.16 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 5.97K | ± 219.65 | ops/s | 9.8x slower |
| openTelemetryInc | 1.42K | ± 137.36 | ops/s | 41x slower |
| openTelemetryAdd | 1.33K | ± 24.79 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.30K | ± 85.76 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.09K | ± 1.26K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 93.16 | ops/s | 1.3x slower |
| prometheusNative | 2.73K | ± 53.98 | ops/s | 2.2x slower |
| openTelemetryClassic | 621.15 | ± 23.94 | ops/s | 9.8x slower |
| openTelemetryExponential | 526.16 | ± 27.49 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 545.34K | ± 10.34K | ops/s | **fastest** |
| prometheusWriteToByteArray | 538.68K | ± 5.04K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 516.01K | ± 9.24K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 512.49K | ± 7.11K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44619.426    ± 610.513  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1326.128     ± 24.790  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1420.519    ± 137.357  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1303.449     ± 85.756  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48917.828    ± 660.375  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58634.992   ± 2857.757  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51855.479    ± 834.068  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5992.020    ± 152.155  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6151.161    ± 104.261  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5973.475    ± 219.650  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        621.150     ± 23.939  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        526.158     ± 27.491  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6089.716   ± 1262.576  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2729.022     ± 53.978  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4546.166     ± 93.162  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     512490.437   ± 7108.279  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     516008.731   ± 9244.577  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     538682.053   ± 5041.990  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     545336.064  ± 10339.432  ops/s
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
