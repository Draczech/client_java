# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-13T05:17:40Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.26K | ± 2.99K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.69K | ± 317.93 | ops/s | 1.1x slower |
| prometheusAdd | 51.31K | ± 541.26 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.41K | ± 447.71 | ops/s | 1.3x slower |
| simpleclientInc | 6.46K | ± 61.84 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.38K | ± 167.28 | ops/s | 10x slower |
| simpleclientAdd | 6.12K | ± 77.20 | ops/s | 11x slower |
| openTelemetryAdd | 1.47K | ± 278.60 | ops/s | 44x slower |
| openTelemetryInc | 1.30K | ± 8.94 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.21K | ± 13.52 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.62K | ± 498.49 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 50.18 | ops/s | 1.0x slower |
| prometheusNative | 2.93K | ± 295.28 | ops/s | 1.6x slower |
| openTelemetryClassic | 665.53 | ± 18.44 | ops/s | 6.9x slower |
| openTelemetryExponential | 559.67 | ± 23.77 | ops/s | 8.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 479.30K | ± 7.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 474.03K | ± 8.95K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.46K | ± 4.74K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 462.60K | ± 6.51K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50407.993    ± 447.713  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1473.170    ± 278.599  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1300.265      ± 8.941  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1209.031     ± 13.517  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51306.141    ± 541.258  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64263.334   ± 2994.185  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56694.485    ± 317.933  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6119.714     ± 77.200  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6458.759     ± 61.836  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6377.063    ± 167.285  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        665.531     ± 18.437  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.671     ± 23.772  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4615.436    ± 498.489  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2934.658    ± 295.281  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4546.829     ± 50.180  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466459.819   ± 4742.332  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     462603.164   ± 6508.319  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     474034.630   ± 8946.191  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     479304.073   ± 7601.385  ops/s
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
