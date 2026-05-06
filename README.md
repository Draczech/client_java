# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-06T06:33:56Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.33K | ± 2.48K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.40K | ± 439.93 | ops/s | 1.1x slower |
| prometheusAdd | 46.62K | ± 2.26K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.30K | ± 318.80 | ops/s | 1.3x slower |
| simpleclientInc | 6.30K | ± 76.56 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.10K | ± 304.73 | ops/s | 9.6x slower |
| simpleclientAdd | 5.83K | ± 295.45 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 100.52 | ops/s | 41x slower |
| openTelemetryInc | 1.41K | ± 178.68 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.18K | ± 192.54 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.15K | ± 1.16K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 97.08 | ops/s | 1.2x slower |
| prometheusNative | 3.09K | ± 134.42 | ops/s | 1.7x slower |
| openTelemetryClassic | 643.83 | ± 25.16 | ops/s | 8.0x slower |
| openTelemetryExponential | 530.35 | ± 27.93 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 537.76K | ± 6.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 523.14K | ± 5.17K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 514.32K | ± 8.56K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 500.99K | ± 4.65K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44297.698    ± 318.801  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1426.258    ± 100.520  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1410.854    ± 178.676  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1177.206    ± 192.545  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      46617.596   ± 2260.318  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58329.884   ± 2480.601  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51404.738    ± 439.934  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5826.245    ± 295.446  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6295.242     ± 76.564  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6101.182    ± 304.731  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        643.826     ± 25.157  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        530.346     ± 27.925  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5150.687   ± 1159.522  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3093.079    ± 134.423  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4473.785     ± 97.075  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     500993.063   ± 4654.592  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514320.027   ± 8556.110  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     523137.279   ± 5168.383  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     537761.396   ± 6012.335  ops/s
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
