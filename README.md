# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-02T07:47:39Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.61K | ± 1.53K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.59K | ± 441.31 | ops/s | 1.2x slower |
| prometheusAdd | 51.30K | ± 305.43 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.10K | ± 191.60 | ops/s | 1.4x slower |
| simpleclientInc | 6.52K | ± 162.40 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.33K | ± 198.70 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 362.89 | ops/s | 11x slower |
| openTelemetryInc | 1.61K | ± 81.49 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.49K | ± 238.82 | ops/s | 44x slower |
| openTelemetryAdd | 1.42K | ± 268.70 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 1.19K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 49.93 | ops/s | 1.2x slower |
| prometheusNative | 2.66K | ± 67.31 | ops/s | 2.0x slower |
| openTelemetryClassic | 697.99 | ± 27.84 | ops/s | 7.7x slower |
| openTelemetryExponential | 544.44 | ± 43.48 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.95K | ± 2.43K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.74K | ± 3.46K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.48K | ± 3.15K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.90K | ± 2.52K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47099.560    ± 191.600  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1417.771    ± 268.703  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1609.818     ± 81.488  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1486.870    ± 238.817  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51303.231    ± 305.426  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65614.068   ± 1526.625  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56588.927    ± 441.314  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6225.910    ± 362.887  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6524.567    ± 162.399  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6333.159    ± 198.699  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        697.992     ± 27.840  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.442     ± 43.482  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5362.339   ± 1193.893  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2656.798     ± 67.308  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4443.600     ± 49.932  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470896.731   ± 2517.053  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478480.338   ± 3151.842  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487736.381   ± 3463.170  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489951.529   ± 2432.032  ops/s
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
