# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-29T06:12:22Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.66K | ± 1.16K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.12K | ± 675.01 | ops/s | 1.2x slower |
| prometheusAdd | 47.46K | ± 2.07K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.19K | ± 182.87 | ops/s | 1.4x slower |
| simpleclientInc | 6.24K | ± 145.16 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.13K | ± 262.44 | ops/s | 9.7x slower |
| simpleclientAdd | 5.69K | ± 190.58 | ops/s | 10x slower |
| openTelemetryInc | 1.37K | ± 59.41 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.35K | ± 65.09 | ops/s | 44x slower |
| openTelemetryAdd | 1.31K | ± 51.61 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.40K | ± 1.30K | ops/s | **fastest** |
| simpleclient | 4.35K | ± 35.45 | ops/s | 1.7x slower |
| prometheusNative | 2.84K | ± 242.12 | ops/s | 2.6x slower |
| openTelemetryClassic | 569.79 | ± 14.97 | ops/s | 13x slower |
| openTelemetryExponential | 513.68 | ± 25.97 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 553.88K | ± 2.46K | ops/s | **fastest** |
| prometheusWriteToByteArray | 542.52K | ± 3.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 532.69K | ± 4.71K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 521.38K | ± 3.66K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44192.711    ± 182.875  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1312.316     ± 51.606  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1366.010     ± 59.414  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1352.452     ± 65.086  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47462.444   ± 2068.773  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59663.477   ± 1156.836  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51115.239    ± 675.012  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5692.278    ± 190.584  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6244.075    ± 145.155  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6127.278    ± 262.439  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        569.786     ± 14.968  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        513.685     ± 25.970  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7402.179   ± 1300.230  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2841.560    ± 242.125  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4348.157     ± 35.450  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     521381.324   ± 3663.696  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     532686.580   ± 4714.930  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     542517.473   ± 3676.549  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     553882.112   ± 2462.364  ops/s
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
