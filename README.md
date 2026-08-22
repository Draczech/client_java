# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-22T04:00:44Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.78K | ± 1.88K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.64K | ± 619.26 | ops/s | 1.2x slower |
| prometheusAdd | 51.45K | ± 206.93 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.84K | ± 2.14K | ops/s | 1.4x slower |
| simpleclientInc | 6.62K | ± 91.30 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.51K | ± 126.25 | ops/s | 10x slower |
| simpleclientAdd | 6.00K | ± 26.41 | ops/s | 11x slower |
| openTelemetryAdd | 1.61K | ± 300.32 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.44K | ± 62.60 | ops/s | 46x slower |
| openTelemetryInc | 1.35K | ± 165.31 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.49K | ± 1.43K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 49.74 | ops/s | 1.2x slower |
| prometheusNative | 2.95K | ± 263.14 | ops/s | 1.9x slower |
| openTelemetryClassic | 715.19 | ± 28.99 | ops/s | 7.7x slower |
| openTelemetryExponential | 569.51 | ± 22.87 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 482.96K | ± 3.99K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.47K | ± 3.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.88K | ± 1.29K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.63K | ± 5.32K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47840.754   ± 2136.183  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1614.410    ± 300.317  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1352.121    ± 165.312  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1441.413     ± 62.603  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51445.773    ± 206.933  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65782.626   ± 1877.218  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56643.824    ± 619.264  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6002.339     ± 26.408  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6618.947     ± 91.296  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6510.267    ± 126.252  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        715.188     ± 28.991  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.512     ± 22.869  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5486.811   ± 1432.337  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2949.921    ± 263.135  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4432.501     ± 49.735  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464633.972   ± 5318.107  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477878.672   ± 1294.366  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481466.298   ± 3695.334  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482963.677   ± 3990.434  ops/s
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
