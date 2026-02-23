# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-23T05:27:56Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.62K | ± 25.86 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.98K | ± 179.75 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.01K | ± 1.26K | ops/s | 1.1x slower |
| prometheusAdd | 27.59K | ± 1.46K | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 7.07K | ± 65.71 | ops/s | 4.5x slower |
| simpleclientInc | 6.99K | ± 60.54 | ops/s | 4.5x slower |
| simpleclientAdd | 6.65K | ± 130.80 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.53K | ± 23.99 | ops/s | 21x slower |
| openTelemetryInc | 1.48K | ± 74.41 | ops/s | 21x slower |
| openTelemetryAdd | 1.45K | ± 123.64 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.54K | ± 27.15 | ops/s | **fastest** |
| prometheusClassic | 3.00K | ± 385.01 | ops/s | 1.5x slower |
| prometheusNative | 2.21K | ± 190.77 | ops/s | 2.1x slower |
| openTelemetryClassic | 539.99 | ± 32.89 | ops/s | 8.4x slower |
| openTelemetryExponential | 394.68 | ± 13.52 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 315.99K | ± 2.03K | ops/s | **fastest** |
| prometheusWriteToByteArray | 314.03K | ± 1.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 294.75K | ± 2.38K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 292.78K | ± 3.14K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29011.848   ± 1259.526  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1454.843    ± 123.638  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1479.925     ± 74.411  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1534.022     ± 23.988  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27588.005   ± 1456.320  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31620.644     ± 25.859  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30981.132    ± 179.751  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6654.276    ± 130.796  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6991.334     ± 60.540  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7072.472     ± 65.705  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        539.992     ± 32.891  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        394.683     ± 13.519  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3003.572    ± 385.011  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2205.815    ± 190.772  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4542.225     ± 27.152  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     292780.477   ± 3138.646  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     294754.287   ± 2383.944  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     314027.709   ± 1430.966  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     315993.942   ± 2026.154  ops/s
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
