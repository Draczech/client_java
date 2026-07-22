# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-22T06:11:26Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.63K | ± 1.40K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.33K | ± 2.04K | ops/s | 1.2x slower |
| prometheusAdd | 51.18K | ± 259.54 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 41.27K | ± 14.83K | ops/s | 1.6x slower |
| simpleclientInc | 6.52K | ± 66.11 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.52K | ± 216.74 | ops/s | 9.9x slower |
| simpleclientAdd | 6.34K | ± 183.05 | ops/s | 10x slower |
| openTelemetryAdd | 1.53K | ± 419.80 | ops/s | 42x slower |
| openTelemetryInc | 1.48K | ± 224.61 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.39K | ± 232.51 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.14K | ± 1.90K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 96.46 | ops/s | 1.4x slower |
| prometheusNative | 3.11K | ± 233.25 | ops/s | 2.0x slower |
| openTelemetryClassic | 705.82 | ± 42.58 | ops/s | 8.7x slower |
| openTelemetryExponential | 561.04 | ± 19.85 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.13K | ± 3.13K | ops/s | **fastest** |
| prometheusWriteToByteArray | 476.94K | ± 6.76K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 474.34K | ± 5.31K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 456.04K | ± 5.85K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      41270.113  ± 14827.088  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1526.858    ± 419.797  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1483.600    ± 224.611  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1387.719    ± 232.508  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51179.851    ± 259.539  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64630.297   ± 1400.641  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54325.654   ± 2042.296  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6335.221    ± 183.049  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6517.454     ± 66.114  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6515.267    ± 216.736  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        705.817     ± 42.576  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.039     ± 19.846  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6135.950   ± 1899.098  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3110.062    ± 233.249  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4463.735     ± 96.457  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     456043.570   ± 5845.023  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474344.094   ± 5311.801  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     476941.355   ± 6763.530  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485132.700   ± 3131.790  ops/s
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
