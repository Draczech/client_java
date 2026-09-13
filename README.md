# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-13T08:09:22Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.44K | ± 616.48 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.48K | ± 178.62 | ops/s | 1.2x slower |
| prometheusAdd | 50.97K | ± 600.75 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.28K | ± 675.73 | ops/s | 1.4x slower |
| simpleclientInc | 6.49K | ± 208.27 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 202.47 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.30K | ± 50.79 | ops/s | 11x slower |
| openTelemetryInc | 1.30K | ± 221.70 | ops/s | 51x slower |
| openTelemetryAdd | 1.29K | ± 55.75 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.20K | ± 50.99 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 963.71 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 45.03 | ops/s | 1.2x slower |
| prometheusNative | 3.16K | ± 76.49 | ops/s | 1.7x slower |
| openTelemetryClassic | 721.54 | ± 13.83 | ops/s | 7.3x slower |
| openTelemetryExponential | 566.71 | ± 35.77 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.96K | ± 4.92K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.76K | ± 2.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.96K | ± 6.43K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.19K | ± 7.67K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48280.634    ± 675.725  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1291.128     ± 55.753  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1303.706    ± 221.700  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1197.429     ± 50.995  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50973.006    ± 600.748  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66438.348    ± 616.484  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56479.639    ± 178.619  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6337.441    ± 202.468  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6491.466    ± 208.266  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6299.693     ± 50.790  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        721.538     ± 13.826  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.705     ± 35.771  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5262.161    ± 963.714  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3162.877     ± 76.494  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4435.083     ± 45.030  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471193.908   ± 7674.411  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478959.369   ± 6433.447  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487760.739   ± 2259.740  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492958.919   ± 4923.544  ops/s
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
