# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-23T06:46:59Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.03K | ± 929.63 | ops/s | **fastest** |
| prometheusNoLabelsInc | 49.66K | ± 2.22K | ops/s | 1.2x slower |
| prometheusAdd | 47.80K | ± 189.89 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.72K | ± 1.63K | ops/s | 1.4x slower |
| simpleclientInc | 6.31K | ± 31.23 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.25K | ± 10.71 | ops/s | 9.6x slower |
| simpleclientAdd | 6.05K | ± 177.47 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.35K | ± 78.31 | ops/s | 44x slower |
| openTelemetryAdd | 1.25K | ± 9.68 | ops/s | 48x slower |
| openTelemetryInc | 1.23K | ± 58.96 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.50K | ± 970.47 | ops/s | **fastest** |
| simpleclient | 4.33K | ± 56.07 | ops/s | 1.5x slower |
| prometheusNative | 2.98K | ± 272.93 | ops/s | 2.2x slower |
| openTelemetryClassic | 592.40 | ± 17.68 | ops/s | 11x slower |
| openTelemetryExponential | 490.99 | ± 9.37 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 560.56K | ± 3.12K | ops/s | **fastest** |
| prometheusWriteToByteArray | 543.30K | ± 4.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 536.38K | ± 2.45K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 519.54K | ± 6.85K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43721.524   ± 1629.111  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1252.875      ± 9.680  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1234.090     ± 58.959  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1349.173     ± 78.314  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47804.254    ± 189.886  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60029.079    ± 929.633  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      49659.417   ± 2224.016  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6054.298    ± 177.471  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6312.385     ± 31.233  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6247.868     ± 10.712  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        592.400     ± 17.683  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        490.987      ± 9.374  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6499.457    ± 970.473  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2978.659    ± 272.928  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4334.889     ± 56.075  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     519544.750   ± 6852.542  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     536376.597   ± 2453.827  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     543295.288   ± 4118.334  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     560559.006   ± 3117.855  ops/s
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
