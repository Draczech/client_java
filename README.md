# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-25T08:02:42Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.42K | ± 699.13 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.69K | ± 370.56 | ops/s | 1.2x slower |
| prometheusAdd | 51.34K | ± 229.84 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.23K | ± 1.49K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 167.62 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.47K | ± 171.24 | ops/s | 10x slower |
| simpleclientAdd | 6.27K | ± 225.47 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.34K | ± 140.68 | ops/s | 49x slower |
| openTelemetryInc | 1.26K | ± 32.26 | ops/s | 53x slower |
| openTelemetryAdd | 1.25K | ± 44.32 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.52K | ± 921.29 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 66.10 | ops/s | 1.5x slower |
| prometheusNative | 3.02K | ± 286.87 | ops/s | 2.2x slower |
| openTelemetryClassic | 668.81 | ± 6.49 | ops/s | 9.7x slower |
| openTelemetryExponential | 554.70 | ± 11.86 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.01K | ± 2.28K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.43K | ± 3.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.45K | ± 6.53K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.13K | ± 10.59K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48232.614   ± 1487.837  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1246.741     ± 44.322  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1255.212     ± 32.264  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1343.302    ± 140.679  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51338.244    ± 229.837  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66417.275    ± 699.135  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56693.483    ± 370.560  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6268.622    ± 225.470  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6589.684    ± 167.625  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6468.943    ± 171.240  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        668.810      ± 6.488  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.697     ± 11.857  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6517.120    ± 921.290  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3023.144    ± 286.869  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4445.004     ± 66.099  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474134.421  ± 10589.271  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478451.796   ± 6531.200  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482427.187   ± 3920.417  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491006.661   ± 2275.404  ops/s
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
