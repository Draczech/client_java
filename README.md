# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-20T07:24:15Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.01K | ± 346.96 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.91K | ± 317.21 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.16K | ± 1.56K | ops/s | 1.3x slower |
| prometheusAdd | 48.74K | ± 3.85K | ops/s | 1.4x slower |
| simpleclientInc | 6.53K | ± 168.80 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.39K | ± 177.12 | ops/s | 10x slower |
| simpleclientAdd | 6.07K | ± 307.67 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.30K | ± 189.51 | ops/s | 51x slower |
| openTelemetryAdd | 1.29K | ± 141.17 | ops/s | 51x slower |
| openTelemetryInc | 1.26K | ± 45.16 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.52K | ± 1.11K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 86.86 | ops/s | 1.5x slower |
| prometheusNative | 2.79K | ± 275.85 | ops/s | 2.3x slower |
| openTelemetryClassic | 660.51 | ± 34.33 | ops/s | 9.9x slower |
| openTelemetryExponential | 585.36 | ± 16.95 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 483.42K | ± 6.91K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.39K | ± 5.52K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.27K | ± 2.29K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.72K | ± 5.01K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49163.575   ± 1564.591  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1286.974    ± 141.175  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1261.805     ± 45.159  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1295.417    ± 189.512  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48740.255   ± 3845.750  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66009.205    ± 346.958  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56906.400    ± 317.213  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6067.684    ± 307.669  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6525.045    ± 168.799  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6393.577    ± 177.117  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        660.505     ± 34.330  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        585.357     ± 16.953  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6524.866   ± 1108.965  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2794.360    ± 275.855  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4432.959     ± 86.864  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475723.117   ± 5005.346  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476273.071   ± 2285.068  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481389.296   ± 5518.198  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     483421.048   ± 6913.155  ops/s
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
