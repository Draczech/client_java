# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-05T06:07:17Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.69K | ± 2.46K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.56K | ± 451.67 | ops/s | 1.1x slower |
| prometheusAdd | 46.28K | ± 2.29K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 41.92K | ± 1.49K | ops/s | 1.4x slower |
| simpleclientInc | 6.16K | ± 124.32 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 5.98K | ± 255.86 | ops/s | 9.8x slower |
| simpleclientAdd | 5.97K | ± 373.18 | ops/s | 9.8x slower |
| openTelemetryInc | 1.40K | ± 81.44 | ops/s | 42x slower |
| openTelemetryAdd | 1.39K | ± 99.50 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.33K | ± 59.02 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.48K | ± 1.59K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 38.47 | ops/s | 1.5x slower |
| prometheusNative | 3.18K | ± 52.84 | ops/s | 2.0x slower |
| openTelemetryClassic | 623.40 | ± 39.18 | ops/s | 10x slower |
| openTelemetryExponential | 525.03 | ± 5.80 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 533.82K | ± 5.39K | ops/s | **fastest** |
| prometheusWriteToByteArray | 523.20K | ± 3.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 509.31K | ± 4.28K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 505.26K | ± 8.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      41923.191   ± 1485.467  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1385.545     ± 99.500  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1404.510     ± 81.440  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1326.221     ± 59.024  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      46277.544   ± 2287.455  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58692.312   ± 2462.619  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51556.502    ± 451.665  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5972.868    ± 373.182  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6158.135    ± 124.319  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5982.056    ± 255.858  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        623.402     ± 39.183  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        525.034      ± 5.804  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6478.050   ± 1590.390  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3177.888     ± 52.842  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4406.209     ± 38.467  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     505261.412   ± 8203.995  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509313.597   ± 4278.586  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     523198.131   ± 3554.322  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     533822.862   ± 5387.148  ops/s
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
