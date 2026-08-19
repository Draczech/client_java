# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-19T04:03:47Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.47K | ± 2.13K | ops/s | **fastest** |
| prometheusNoLabelsInc | 49.92K | ± 2.94K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.29K | ± 454.07 | ops/s | 1.3x slower |
| prometheusAdd | 41.92K | ± 10.79K | ops/s | 1.4x slower |
| simpleclientInc | 6.34K | ± 28.27 | ops/s | 9.1x slower |
| simpleclientNoLabelsInc | 5.90K | ± 57.01 | ops/s | 9.7x slower |
| simpleclientAdd | 5.69K | ± 340.41 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.44K | ± 88.58 | ops/s | 40x slower |
| openTelemetryAdd | 1.40K | ± 149.66 | ops/s | 41x slower |
| openTelemetryInc | 1.38K | ± 119.03 | ops/s | 42x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.00K | ± 2.07K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 50.09 | ops/s | 1.4x slower |
| prometheusNative | 3.20K | ± 80.54 | ops/s | 1.9x slower |
| openTelemetryClassic | 588.01 | ± 22.42 | ops/s | 10x slower |
| openTelemetryExponential | 514.89 | ± 32.15 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 548.29K | ± 12.44K | ops/s | **fastest** |
| prometheusWriteToByteArray | 542.78K | ± 6.09K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 533.53K | ± 12.60K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 521.06K | ± 8.58K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44291.825    ± 454.073  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1398.649    ± 149.665  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1377.732    ± 119.025  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1444.680     ± 88.580  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      41918.663  ± 10791.581  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57474.212   ± 2127.506  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      49921.791   ± 2940.306  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5690.652    ± 340.405  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6343.020     ± 28.271  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5898.662     ± 57.008  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        588.013     ± 22.425  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        514.886     ± 32.153  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6000.926   ± 2074.591  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3202.396     ± 80.540  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4411.731     ± 50.087  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     521057.461   ± 8576.716  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     533528.916  ± 12595.816  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     542780.572   ± 6091.242  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     548291.141  ± 12443.137  ops/s
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
