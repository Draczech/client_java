# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-06T07:31:51Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.23K | ± 768.63 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.10K | ± 81.10 | ops/s | 1.2x slower |
| prometheusAdd | 51.54K | ± 200.81 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.61K | ± 845.94 | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 153.01 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.54K | ± 161.87 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 247.88 | ops/s | 10x slower |
| openTelemetryInc | 1.41K | ± 236.02 | ops/s | 47x slower |
| openTelemetryAdd | 1.34K | ± 149.00 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.30K | ± 227.14 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.99K | ± 2.45K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 70.25 | ops/s | 1.6x slower |
| prometheusNative | 3.05K | ± 280.62 | ops/s | 2.3x slower |
| openTelemetryClassic | 697.16 | ± 54.59 | ops/s | 10x slower |
| openTelemetryExponential | 533.00 | ± 30.66 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.17K | ± 5.06K | ops/s | **fastest** |
| openMetricsWriteToNull | 489.85K | ± 3.31K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 486.33K | ± 3.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.77K | ± 3.40K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50607.265    ± 845.939  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1340.951    ± 148.997  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1406.871    ± 236.018  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1296.266    ± 227.139  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51543.251    ± 200.814  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66231.852    ± 768.629  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57097.733     ± 81.095  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6320.631    ± 247.881  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6550.607    ± 153.006  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6544.865    ± 161.870  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        697.158     ± 54.590  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        532.997     ± 30.659  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6992.168   ± 2448.297  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3048.667    ± 280.621  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4409.924     ± 70.248  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477767.618   ± 3402.144  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489853.416   ± 3313.094  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486333.753   ± 3550.441  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496166.180   ± 5062.485  ops/s
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
