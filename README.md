# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-30T06:36:27Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.40K | ± 830.86 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.83K | ± 160.21 | ops/s | 1.2x slower |
| prometheusAdd | 48.69K | ± 841.17 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 45.02K | ± 656.32 | ops/s | 1.3x slower |
| simpleclientInc | 6.18K | ± 146.81 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.13K | ± 257.36 | ops/s | 9.9x slower |
| simpleclientAdd | 5.93K | ± 212.66 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.49K | ± 86.59 | ops/s | 40x slower |
| openTelemetryInc | 1.38K | ± 9.76 | ops/s | 44x slower |
| openTelemetryAdd | 1.34K | ± 31.58 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.11K | ± 1.76K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 76.60 | ops/s | 1.6x slower |
| prometheusNative | 2.93K | ± 181.15 | ops/s | 2.4x slower |
| openTelemetryClassic | 632.80 | ± 28.71 | ops/s | 11x slower |
| openTelemetryExponential | 530.30 | ± 27.83 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.26K | ± 2.33K | ops/s | **fastest** |
| prometheusWriteToByteArray | 544.02K | ± 2.32K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.75K | ± 2.46K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 520.05K | ± 7.80K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45024.789    ± 656.324  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1336.602     ± 31.579  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1384.739      ± 9.757  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1493.406     ± 86.586  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48692.241    ± 841.167  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60400.717    ± 830.857  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50828.370    ± 160.213  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5932.473    ± 212.664  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6175.446    ± 146.811  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6128.705    ± 257.361  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        632.797     ± 28.709  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        530.297     ± 27.831  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7107.703   ± 1760.636  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2932.752    ± 181.152  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4555.208     ± 76.605  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     520048.347   ± 7796.477  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534746.450   ± 2457.780  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     544023.212   ± 2320.956  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555261.111   ± 2334.220  ops/s
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
