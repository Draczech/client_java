# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-09T08:05:30Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.75K | ± 1.79K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.24K | ± 1.03K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.25K | ± 1.54K | ops/s | 1.3x slower |
| prometheusAdd | 48.17K | ± 3.98K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.59K | ± 15.08 | ops/s | 10.0x slower |
| simpleclientInc | 6.56K | ± 145.77 | ops/s | 10x slower |
| simpleclientAdd | 6.03K | ± 338.34 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.40K | ± 114.30 | ops/s | 47x slower |
| openTelemetryInc | 1.35K | ± 122.09 | ops/s | 49x slower |
| openTelemetryAdd | 1.29K | ± 37.60 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.44K | ± 1.10K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 49.12 | ops/s | 1.5x slower |
| prometheusNative | 2.97K | ± 229.01 | ops/s | 2.2x slower |
| openTelemetryClassic | 693.66 | ± 24.29 | ops/s | 9.3x slower |
| openTelemetryExponential | 550.38 | ± 18.45 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 487.71K | ± 3.92K | ops/s | **fastest** |
| prometheusWriteToNull | 487.71K | ± 2.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.93K | ± 4.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.76K | ± 9.19K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49250.661   ± 1540.615  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1285.964     ± 37.595  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1352.787    ± 122.089  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1396.276    ± 114.305  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48167.559   ± 3978.002  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65746.739   ± 1788.244  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56235.199   ± 1032.837  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6033.541    ± 338.343  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6564.134    ± 145.770  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6593.988     ± 15.077  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        693.661     ± 24.291  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.379     ± 18.450  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6437.858   ± 1098.188  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2966.221    ± 229.009  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4418.659     ± 49.122  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477757.604   ± 9192.768  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480931.701   ± 4607.621  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487713.001   ± 3924.768  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487709.775   ± 2272.349  ops/s
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
