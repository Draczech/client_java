# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-16T05:58:15Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.90K | ± 724.47 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.99K | ± 933.66 | ops/s | 1.2x slower |
| prometheusAdd | 48.75K | ± 934.82 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.31K | ± 223.93 | ops/s | 1.4x slower |
| simpleclientInc | 6.25K | ± 119.83 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.97K | ± 210.18 | ops/s | 10x slower |
| simpleclientAdd | 5.90K | ± 276.18 | ops/s | 10x slower |
| openTelemetryAdd | 1.34K | ± 82.62 | ops/s | 46x slower |
| openTelemetryInc | 1.24K | ± 47.63 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.22K | ± 53.68 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.70K | ± 575.29 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 16.01 | ops/s | 1.1x slower |
| prometheusNative | 2.97K | ± 326.43 | ops/s | 1.6x slower |
| openTelemetryClassic | 588.00 | ± 16.79 | ops/s | 8.0x slower |
| openTelemetryExponential | 505.60 | ± 21.80 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 553.87K | ± 4.53K | ops/s | **fastest** |
| prometheusWriteToByteArray | 545.07K | ± 2.05K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.66K | ± 6.44K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 518.99K | ± 6.12K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44306.284    ± 223.933  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1337.552     ± 82.622  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1235.597     ± 47.633  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1220.798     ± 53.677  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48753.877    ± 934.821  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60900.334    ± 724.471  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51989.052    ± 933.655  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5900.783    ± 276.176  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6253.426    ± 119.831  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5973.571    ± 210.179  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        587.998     ± 16.793  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        505.597     ± 21.804  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4696.412    ± 575.289  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2972.824    ± 326.428  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4435.578     ± 16.009  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     518992.051   ± 6119.442  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534664.636   ± 6443.330  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     545069.584   ± 2048.122  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     553873.862   ± 4528.238  ops/s
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
