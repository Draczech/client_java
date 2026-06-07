# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-07T07:27:53Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.55K | ± 1.56K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.09K | ± 921.81 | ops/s | 1.2x slower |
| prometheusAdd | 50.73K | ± 581.45 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.47K | ± 913.32 | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 9.84 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.54K | ± 106.00 | ops/s | 9.9x slower |
| simpleclientAdd | 6.00K | ± 60.27 | ops/s | 11x slower |
| openTelemetryInc | 1.33K | ± 42.94 | ops/s | 49x slower |
| openTelemetryAdd | 1.26K | ± 69.98 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.22K | ± 22.14 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.21K | ± 1.13K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 47.23 | ops/s | 1.4x slower |
| prometheusNative | 3.05K | ± 352.33 | ops/s | 2.0x slower |
| openTelemetryClassic | 718.52 | ± 58.66 | ops/s | 8.6x slower |
| openTelemetryExponential | 535.82 | ± 21.60 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 483.53K | ± 7.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.87K | ± 3.31K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.98K | ± 3.31K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.50K | ± 2.73K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49472.824    ± 913.321  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1262.518     ± 69.976  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1329.862     ± 42.941  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1215.178     ± 22.137  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50733.218    ± 581.446  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64553.973   ± 1560.460  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56089.688    ± 921.806  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5998.553     ± 60.268  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6700.099      ± 9.843  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6542.407    ± 106.000  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        718.517     ± 58.664  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        535.818     ± 21.601  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6206.618   ± 1133.867  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3047.707    ± 352.335  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4459.731     ± 47.229  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471501.434   ± 2727.378  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473980.597   ± 3309.707  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481870.041   ± 3310.879  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     483526.772   ± 7194.686  ops/s
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
