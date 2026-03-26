# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-26T05:38:58Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.49K | ± 1.63K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.70K | ± 592.81 | ops/s | 1.2x slower |
| prometheusAdd | 51.34K | ± 379.87 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.14K | ± 2.52K | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 14.71 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.41K | ± 174.65 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 332.67 | ops/s | 11x slower |
| openTelemetryInc | 1.42K | ± 227.14 | ops/s | 46x slower |
| openTelemetryAdd | 1.40K | ± 223.86 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.25K | ± 19.33 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.58K | ± 1.27K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 18.07 | ops/s | 1.2x slower |
| prometheusNative | 2.82K | ± 279.98 | ops/s | 2.0x slower |
| openTelemetryClassic | 705.87 | ± 25.23 | ops/s | 7.9x slower |
| openTelemetryExponential | 561.38 | ± 21.62 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.24K | ± 4.48K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.22K | ± 7.25K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.41K | ± 6.25K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.63K | ± 8.47K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50142.680   ± 2517.731  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1401.576    ± 223.857  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1424.423    ± 227.143  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1245.826     ± 19.335  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51335.608    ± 379.873  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65486.381   ± 1628.294  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56701.059    ± 592.811  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6234.199    ± 332.673  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6700.240     ± 14.712  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6409.068    ± 174.653  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        705.866     ± 25.232  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.378     ± 21.622  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5582.633   ± 1268.965  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2822.929    ± 279.981  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4524.782     ± 18.069  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477626.223   ± 8474.833  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486413.178   ± 6253.839  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489223.305   ± 7251.217  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496239.504   ± 4476.073  ops/s
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
