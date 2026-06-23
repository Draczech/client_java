# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-23T07:13:21Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.87K | ± 179.85 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.14K | ± 560.50 | ops/s | 1.1x slower |
| prometheusAdd | 48.27K | ± 197.74 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.21K | ± 235.97 | ops/s | 1.4x slower |
| simpleclientInc | 6.24K | ± 123.45 | ops/s | 9.6x slower |
| simpleclientAdd | 6.12K | ± 47.96 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.02K | ± 174.83 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.41K | ± 108.96 | ops/s | 42x slower |
| openTelemetryInc | 1.33K | ± 97.27 | ops/s | 45x slower |
| openTelemetryAdd | 1.31K | ± 25.97 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.28K | ± 1.70K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 71.89 | ops/s | 1.4x slower |
| prometheusNative | 3.22K | ± 89.52 | ops/s | 2.0x slower |
| openTelemetryClassic | 601.23 | ± 18.63 | ops/s | 10x slower |
| openTelemetryExponential | 513.22 | ± 18.69 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 540.87K | ± 6.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 531.38K | ± 4.19K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 514.77K | ± 668.62 | ops/s | 1.1x slower |
| openMetricsWriteToNull | 514.72K | ± 10.42K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44213.737    ± 235.973  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1308.832     ± 25.975  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1328.457     ± 97.269  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1410.534    ± 108.955  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48266.841    ± 197.743  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59871.647    ± 179.846  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52144.131    ± 560.499  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6124.572     ± 47.960  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6239.864    ± 123.455  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6024.299    ± 174.829  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        601.233     ± 18.630  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        513.217     ± 18.692  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6276.404   ± 1701.318  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3215.860     ± 89.515  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4538.555     ± 71.889  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     514767.619    ± 668.623  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     514718.383  ± 10421.907  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     531379.218   ± 4189.570  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     540870.583   ± 6296.138  ops/s
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
