# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-27T13:21:54Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.83K | ± 722.35 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.14K | ± 922.98 | ops/s | 1.2x slower |
| prometheusAdd | 50.99K | ± 782.43 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 39.91K | ± 13.73K | ops/s | 1.6x slower |
| simpleclientInc | 6.56K | ± 207.07 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 179.33 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.28K | ± 81.03 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.32K | ± 143.73 | ops/s | 50x slower |
| openTelemetryInc | 1.25K | ± 57.49 | ops/s | 53x slower |
| openTelemetryAdd | 1.18K | ± 68.03 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.23K | ± 1.07K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 35.34 | ops/s | 1.4x slower |
| prometheusNative | 2.91K | ± 201.23 | ops/s | 2.1x slower |
| openTelemetryClassic | 702.56 | ± 56.20 | ops/s | 8.9x slower |
| openTelemetryExponential | 565.04 | ± 10.01 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.41K | ± 2.59K | ops/s | **fastest** |
| prometheusWriteToByteArray | 475.41K | ± 6.77K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 463.99K | ± 5.97K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 456.12K | ± 2.82K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      39912.182  ± 13728.198  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1184.710     ± 68.025  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1248.920     ± 57.493  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1318.030    ± 143.730  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50987.018    ± 782.429  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65834.720    ± 722.355  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56140.605    ± 922.984  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6324.497    ± 179.332  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6563.362    ± 207.069  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6283.399     ± 81.031  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        702.561     ± 56.196  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.037     ± 10.007  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6234.397   ± 1066.263  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2912.295    ± 201.228  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4465.429     ± 35.343  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     456122.533   ± 2818.808  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     463989.611   ± 5972.647  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     475413.163   ± 6767.705  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485409.016   ± 2588.488  ops/s
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
