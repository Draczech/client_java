# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-05T05:17:38Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.50K | ± 485.82 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.00K | ± 333.86 | ops/s | 1.2x slower |
| prometheusAdd | 51.18K | ± 742.69 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.85K | ± 1.15K | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 120.46 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.58K | ± 188.81 | ops/s | 10x slower |
| simpleclientAdd | 6.27K | ± 105.75 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.40K | ± 213.79 | ops/s | 47x slower |
| openTelemetryInc | 1.39K | ± 240.00 | ops/s | 48x slower |
| openTelemetryAdd | 1.33K | ± 57.51 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.81K | ± 1.41K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 53.68 | ops/s | 1.3x slower |
| prometheusNative | 3.10K | ± 294.60 | ops/s | 1.9x slower |
| openTelemetryClassic | 684.11 | ± 14.31 | ops/s | 8.5x slower |
| openTelemetryExponential | 579.48 | ± 14.23 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 498.92K | ± 2.43K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.58K | ± 3.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.89K | ± 9.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.76K | ± 1.10K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48849.320   ± 1149.980  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1333.380     ± 57.512  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1386.450    ± 240.003  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1401.971    ± 213.793  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51184.250    ± 742.686  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66498.207    ± 485.818  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57000.046    ± 333.860  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6271.060    ± 105.753  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6662.139    ± 120.459  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6580.837    ± 188.811  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        684.114     ± 14.311  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        579.483     ± 14.235  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5807.234   ± 1413.245  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3098.578    ± 294.604  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4504.472     ± 53.677  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477762.084   ± 1104.836  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479891.516   ± 9357.444  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491580.718   ± 3625.174  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     498921.539   ± 2425.606  ops/s
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
