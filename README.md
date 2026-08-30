# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-30T08:51:53Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.43K | ± 2.13K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.41K | ± 1.11K | ops/s | 1.1x slower |
| prometheusAdd | 51.54K | ± 199.84 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.36K | ± 1.15K | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 20.88 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.55K | ± 60.92 | ops/s | 9.8x slower |
| simpleclientAdd | 6.35K | ± 95.32 | ops/s | 10x slower |
| openTelemetryAdd | 1.56K | ± 188.60 | ops/s | 41x slower |
| openTelemetryInc | 1.37K | ± 177.14 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.33K | ± 186.10 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.96K | ± 496.97 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 24.68 | ops/s | 1.1x slower |
| prometheusNative | 2.82K | ± 311.35 | ops/s | 1.8x slower |
| openTelemetryClassic | 719.80 | ± 15.05 | ops/s | 6.9x slower |
| openTelemetryExponential | 566.56 | ± 47.41 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.50K | ± 4.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.98K | ± 2.91K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.30K | ± 5.60K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.89K | ± 6.07K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49361.655   ± 1149.060  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1557.946    ± 188.599  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1373.848    ± 177.137  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1325.103    ± 186.102  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51540.212    ± 199.838  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64434.063   ± 2131.986  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56413.997   ± 1105.541  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6353.304     ± 95.317  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6699.816     ± 20.878  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6549.084     ± 60.924  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        719.804     ± 15.054  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.557     ± 47.414  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4959.899    ± 496.970  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2819.044    ± 311.345  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4478.594     ± 24.679  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474890.217   ± 6072.831  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479297.924   ± 5604.223  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488976.169   ± 2908.027  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493498.433   ± 4940.015  ops/s
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
