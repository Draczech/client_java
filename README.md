# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-25T05:24:36Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.78K | ± 2.94K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.41K | ± 391.72 | ops/s | 1.1x slower |
| prometheusAdd | 48.33K | ± 171.63 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.60K | ± 1.55K | ops/s | 1.3x slower |
| simpleclientInc | 6.45K | ± 46.98 | ops/s | 9.1x slower |
| simpleclientNoLabelsInc | 6.35K | ± 20.25 | ops/s | 9.3x slower |
| simpleclientAdd | 5.79K | ± 370.24 | ops/s | 10x slower |
| openTelemetryAdd | 1.47K | ± 81.53 | ops/s | 40x slower |
| openTelemetryInc | 1.41K | ± 68.45 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.36K | ± 193.63 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.48K | ± 1.59K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 189.10 | ops/s | 1.4x slower |
| prometheusNative | 3.04K | ± 123.14 | ops/s | 2.1x slower |
| openTelemetryClassic | 617.74 | ± 13.90 | ops/s | 10x slower |
| openTelemetryExponential | 535.16 | ± 15.16 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 562.35K | ± 1.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 553.25K | ± 2.34K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 537.55K | ± 7.83K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 529.99K | ± 942.99 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43597.210   ± 1553.009  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1472.792     ± 81.530  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1409.806     ± 68.448  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1360.781    ± 193.635  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48332.775    ± 171.632  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58777.922   ± 2935.221  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51411.615    ± 391.722  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5794.172    ± 370.243  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6449.745     ± 46.978  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6350.439     ± 20.247  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        617.742     ± 13.897  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        535.156     ± 15.164  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6480.495   ± 1586.562  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3038.276    ± 123.137  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4516.233    ± 189.104  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     529991.688    ± 942.994  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     537552.465   ± 7831.114  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     553249.852   ± 2341.673  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     562352.407   ± 1579.914  ops/s
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
