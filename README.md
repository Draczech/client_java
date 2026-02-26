# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-26T05:21:53Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.65K | ± 1.55K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.93K | ± 351.95 | ops/s | 1.1x slower |
| prometheusAdd | 51.65K | ± 135.17 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.99K | ± 1.40K | ops/s | 1.3x slower |
| simpleclientInc | 6.60K | ± 95.99 | ops/s | 9.8x slower |
| simpleclientAdd | 6.54K | ± 29.55 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.54K | ± 216.86 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 1.38K | ± 232.46 | ops/s | 47x slower |
| openTelemetryInc | 1.25K | ± 45.63 | ops/s | 52x slower |
| openTelemetryAdd | 1.25K | ± 91.87 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.03K | ± 793.52 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 35.59 | ops/s | 1.1x slower |
| prometheusNative | 2.54K | ± 34.82 | ops/s | 2.0x slower |
| openTelemetryClassic | 676.09 | ± 17.21 | ops/s | 7.4x slower |
| openTelemetryExponential | 523.04 | ± 6.72 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.75K | ± 3.74K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.22K | ± 4.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.21K | ± 1.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.95K | ± 6.41K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48985.180   ± 1395.078  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1249.058     ± 91.869  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1250.132     ± 45.628  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1382.030    ± 232.464  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51654.285    ± 135.172  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64653.487   ± 1546.637  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56930.131    ± 351.946  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6542.042     ± 29.550  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6604.623     ± 95.986  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6538.622    ± 216.858  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        676.089     ± 17.209  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        523.039      ± 6.718  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5033.677    ± 793.519  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2541.507     ± 34.824  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4538.416     ± 35.588  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467949.073   ± 6409.362  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477206.907   ± 1994.047  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484216.504   ± 4220.068  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485751.943   ± 3744.025  ops/s
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
