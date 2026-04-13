# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-13T06:04:40Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.95K | ± 2.25K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.18K | ± 393.41 | ops/s | 1.1x slower |
| prometheusAdd | 48.43K | ± 882.14 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 40.32K | ± 4.40K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.28K | ± 25.76 | ops/s | 9.2x slower |
| simpleclientInc | 6.05K | ± 41.31 | ops/s | 9.6x slower |
| simpleclientAdd | 5.66K | ± 163.04 | ops/s | 10x slower |
| openTelemetryInc | 1.42K | ± 57.74 | ops/s | 41x slower |
| openTelemetryAdd | 1.34K | ± 27.02 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.32K | ± 62.99 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.28K | ± 519.74 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 76.93 | ops/s | 1.2x slower |
| prometheusNative | 3.16K | ± 165.08 | ops/s | 1.7x slower |
| openTelemetryClassic | 611.74 | ± 11.10 | ops/s | 8.6x slower |
| openTelemetryExponential | 541.56 | ± 35.90 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.08K | ± 5.90K | ops/s | **fastest** |
| openMetricsWriteToNull | 534.13K | ± 4.20K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 533.60K | ± 5.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 523.65K | ± 7.24K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40324.414   ± 4404.365  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1341.041     ± 27.018  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1418.753     ± 57.737  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1323.200     ± 62.985  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48432.618    ± 882.138  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57951.877   ± 2250.957  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52182.093    ± 393.411  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5656.788    ± 163.044  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6046.729     ± 41.313  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6281.710     ± 25.759  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        611.744     ± 11.098  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.557     ± 35.903  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5277.662    ± 519.736  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3162.665    ± 165.085  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4387.735     ± 76.926  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     523645.676   ± 7241.725  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534130.177   ± 4204.073  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     533599.053   ± 5298.182  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556082.759   ± 5902.439  ops/s
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
