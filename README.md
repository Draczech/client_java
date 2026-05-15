# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-15T07:00:46Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.07K | ± 2.48K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.41K | ± 821.49 | ops/s | 1.1x slower |
| prometheusAdd | 48.35K | ± 264.48 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.36K | ± 673.05 | ops/s | 1.3x slower |
| simpleclientInc | 6.26K | ± 59.34 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.11K | ± 217.36 | ops/s | 9.7x slower |
| simpleclientAdd | 5.49K | ± 56.19 | ops/s | 11x slower |
| openTelemetryAdd | 1.34K | ± 88.15 | ops/s | 44x slower |
| openTelemetryInc | 1.32K | ± 85.08 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.21K | ± 76.02 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 1.52K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 84.02 | ops/s | 1.2x slower |
| prometheusNative | 3.01K | ± 273.37 | ops/s | 1.7x slower |
| openTelemetryClassic | 621.78 | ± 19.89 | ops/s | 8.5x slower |
| openTelemetryExponential | 512.87 | ± 7.13 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 551.08K | ± 2.12K | ops/s | **fastest** |
| prometheusWriteToByteArray | 541.04K | ± 3.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 533.03K | ± 3.23K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 520.58K | ± 10.94K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44358.637    ± 673.050  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1342.390     ± 88.151  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1315.967     ± 85.084  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1207.467     ± 76.022  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48346.205    ± 264.479  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59067.981   ± 2476.825  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51407.449    ± 821.486  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5492.249     ± 56.192  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6257.538     ± 59.337  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6108.214    ± 217.362  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        621.785     ± 19.889  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        512.874      ± 7.134  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5259.520   ± 1520.122  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3012.130    ± 273.369  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4516.289     ± 84.022  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     520578.053  ± 10940.441  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     533029.754   ± 3233.487  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     541039.258   ± 3944.220  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     551077.461   ± 2124.265  ops/s
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
