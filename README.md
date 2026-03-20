# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-20T05:19:30Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.28K | ± 635.93 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.08K | ± 368.70 | ops/s | 1.2x slower |
| prometheusAdd | 51.28K | ± 527.76 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.27K | ± 6.77K | ops/s | 1.5x slower |
| simpleclientInc | 6.60K | ± 146.62 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.44K | ± 117.78 | ops/s | 10x slower |
| simpleclientAdd | 6.24K | ± 251.20 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.37K | ± 200.37 | ops/s | 48x slower |
| openTelemetryAdd | 1.30K | ± 75.94 | ops/s | 51x slower |
| openTelemetryInc | 1.25K | ± 25.29 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.94K | ± 407.90 | ops/s | **fastest** |
| simpleclient | 4.52K | ± 31.63 | ops/s | 1.1x slower |
| prometheusNative | 2.86K | ± 260.94 | ops/s | 1.7x slower |
| openTelemetryClassic | 740.43 | ± 7.46 | ops/s | 6.7x slower |
| openTelemetryExponential | 568.13 | ± 9.61 | ops/s | 8.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.91K | ± 1.67K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.16K | ± 2.34K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.99K | ± 4.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.73K | ± 7.15K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43266.903   ± 6768.234  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1301.690     ± 75.940  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1248.373     ± 25.292  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1372.674    ± 200.369  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51282.753    ± 527.757  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66284.988    ± 635.935  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57082.087    ± 368.700  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6237.448    ± 251.201  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6601.222    ± 146.621  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6437.795    ± 117.780  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        740.428      ± 7.462  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        568.127      ± 9.608  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4940.459    ± 407.900  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2863.912    ± 260.943  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4519.301     ± 31.626  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477727.060   ± 7149.806  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486991.213   ± 4304.738  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487160.865   ± 2342.923  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490908.271   ± 1668.614  ops/s
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
