# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-10T05:52:50Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.11K | ± 1.01K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.95K | ± 55.47 | ops/s | 1.2x slower |
| prometheusAdd | 48.50K | ± 981.87 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.00K | ± 1.84K | ops/s | 1.4x slower |
| simpleclientInc | 6.18K | ± 298.36 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.13K | ± 179.72 | ops/s | 9.8x slower |
| simpleclientAdd | 6.07K | ± 198.35 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.45K | ± 87.83 | ops/s | 41x slower |
| openTelemetryInc | 1.32K | ± 120.42 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.26K | ± 61.64 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.37K | ± 367.35 | ops/s | **fastest** |
| simpleclient | 4.18K | ± 20.69 | ops/s | 1.0x slower |
| prometheusNative | 2.97K | ± 239.12 | ops/s | 1.5x slower |
| openTelemetryClassic | 611.56 | ± 23.89 | ops/s | 7.1x slower |
| openTelemetryExponential | 542.04 | ± 16.97 | ops/s | 8.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.53K | ± 3.33K | ops/s | **fastest** |
| prometheusWriteToByteArray | 541.21K | ± 9.51K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 526.57K | ± 5.75K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 522.44K | ± 7.84K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43000.577   ± 1840.042  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1450.989     ± 87.827  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1324.712    ± 120.418  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1261.935     ± 61.643  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48500.668    ± 981.870  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60109.102   ± 1014.396  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51945.025     ± 55.469  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6068.510    ± 198.348  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6178.648    ± 298.361  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6132.397    ± 179.717  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        611.558     ± 23.892  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        542.038     ± 16.970  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4366.815    ± 367.352  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2968.633    ± 239.117  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4182.438     ± 20.686  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     522437.098   ± 7836.685  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     526567.482   ± 5746.878  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     541209.701   ± 9514.283  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556529.149   ± 3331.700  ops/s
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
