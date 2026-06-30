# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-30T07:15:57Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.27K | ± 1.13K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.65K | ± 442.25 | ops/s | 1.1x slower |
| prometheusAdd | 51.22K | ± 800.60 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.25K | ± 1.73K | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 166.58 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.49K | ± 200.68 | ops/s | 9.9x slower |
| simpleclientAdd | 6.22K | ± 189.71 | ops/s | 10x slower |
| openTelemetryAdd | 1.40K | ± 249.41 | ops/s | 46x slower |
| openTelemetryInc | 1.38K | ± 181.68 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.34K | ± 231.44 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.96K | ± 932.40 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 22.81 | ops/s | 1.1x slower |
| prometheusNative | 2.65K | ± 213.87 | ops/s | 1.9x slower |
| openTelemetryClassic | 711.42 | ± 19.94 | ops/s | 7.0x slower |
| openTelemetryExponential | 556.79 | ± 11.71 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.15K | ± 1.38K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.62K | ± 6.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.19K | ± 2.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.72K | ± 3.16K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48246.542   ± 1725.782  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1399.668    ± 249.406  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1381.028    ± 181.680  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1341.287    ± 231.440  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51220.387    ± 800.596  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64273.829   ± 1129.093  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56648.937    ± 442.250  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6216.309    ± 189.711  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6585.440    ± 166.579  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6488.131    ± 200.684  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        711.425     ± 19.941  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.790     ± 11.711  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4960.046    ± 932.399  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2653.143    ± 213.869  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4406.099     ± 22.810  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468720.932   ± 3159.201  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475185.993   ± 2266.588  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479615.314   ± 6405.760  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486148.681   ± 1380.328  ops/s
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
