# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-09T07:14:40Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.64K | ± 1.54K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.50K | ± 2.65K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.07K | ± 1.65K | ops/s | 1.4x slower |
| prometheusAdd | 47.99K | ± 5.18K | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 59.96 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.51K | ± 145.01 | ops/s | 10x slower |
| simpleclientAdd | 6.22K | ± 217.17 | ops/s | 11x slower |
| openTelemetryAdd | 1.44K | ± 201.48 | ops/s | 46x slower |
| openTelemetryInc | 1.34K | ± 189.97 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.24K | ± 31.41 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.42K | ± 24.84 | ops/s | **fastest** |
| prometheusClassic | 4.19K | ± 321.98 | ops/s | 1.1x slower |
| prometheusNative | 2.78K | ± 317.03 | ops/s | 1.6x slower |
| openTelemetryClassic | 694.78 | ± 9.12 | ops/s | 6.4x slower |
| openTelemetryExponential | 546.57 | ± 34.88 | ops/s | 8.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 471.62K | ± 13.33K | ops/s | **fastest** |
| prometheusWriteToByteArray | 455.50K | ± 19.72K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 407.66K | ± 15.53K | ops/s | 1.2x slower |
| openMetricsWriteToByteArray | 391.30K | ± 6.27K | ops/s | 1.2x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48073.841   ± 1654.036  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1435.854    ± 201.481  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1343.335    ± 189.975  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1239.167     ± 31.411  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47993.825   ± 5179.224  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65637.158   ± 1540.243  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55504.730   ± 2651.513  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6216.415    ± 217.174  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6656.749     ± 59.965  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6511.648    ± 145.012  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        694.778      ± 9.116  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.570     ± 34.880  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4189.206    ± 321.975  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2784.659    ± 317.032  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.564     ± 24.842  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     391299.880   ± 6272.420  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     407657.899  ± 15528.565  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     455503.718  ± 19716.558  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     471615.179  ± 13329.094  ops/s
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
