# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-18T05:51:52Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.13K | ± 1.04K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.45K | ± 2.49K | ops/s | 1.2x slower |
| prometheusAdd | 51.63K | ± 58.69 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.37K | ± 1.38K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 212.58 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.33K | ± 206.91 | ops/s | 10x slower |
| simpleclientAdd | 6.24K | ± 206.48 | ops/s | 10x slower |
| openTelemetryInc | 1.37K | ± 201.33 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.31K | ± 177.38 | ops/s | 50x slower |
| openTelemetryAdd | 1.26K | ± 9.96 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.42K | ± 73.00 | ops/s | **fastest** |
| prometheusClassic | 4.02K | ± 186.18 | ops/s | 1.1x slower |
| prometheusNative | 2.62K | ± 88.98 | ops/s | 1.7x slower |
| openTelemetryClassic | 681.58 | ± 24.94 | ops/s | 6.5x slower |
| openTelemetryExponential | 534.94 | ± 9.43 | ops/s | 8.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.29K | ± 4.53K | ops/s | **fastest** |
| prometheusWriteToByteArray | 471.40K | ± 9.45K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 461.05K | ± 13.65K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 457.91K | ± 9.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48367.220   ± 1383.520  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1264.464      ± 9.955  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1374.121    ± 201.325  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1313.521    ± 177.384  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51631.730     ± 58.693  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65126.850   ± 1038.507  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55447.152   ± 2489.364  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6244.069    ± 206.480  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6550.264    ± 212.582  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6333.681    ± 206.910  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        681.582     ± 24.937  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        534.941      ± 9.431  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4018.536    ± 186.176  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2617.803     ± 88.978  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4421.214     ± 73.000  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     461047.702  ± 13648.960  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     457913.964   ± 9553.551  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     471395.437   ± 9451.192  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485287.216   ± 4532.680  ops/s
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
