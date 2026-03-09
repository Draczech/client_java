# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-09T05:21:30Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.78K | ± 4.34K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 376.75 | ops/s | 1.1x slower |
| prometheusAdd | 51.50K | ± 217.52 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.40K | ± 910.92 | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 120.65 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.48K | ± 179.42 | ops/s | 9.8x slower |
| simpleclientAdd | 6.18K | ± 80.60 | ops/s | 10x slower |
| openTelemetryAdd | 1.33K | ± 106.20 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.30K | ± 10.30 | ops/s | 49x slower |
| openTelemetryInc | 1.21K | ± 25.81 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.75K | ± 1.54K | ops/s | **fastest** |
| simpleclient | 4.57K | ± 19.63 | ops/s | 1.3x slower |
| prometheusNative | 2.93K | ± 260.00 | ops/s | 2.0x slower |
| openTelemetryClassic | 671.09 | ± 19.61 | ops/s | 8.6x slower |
| openTelemetryExponential | 575.28 | ± 5.62 | ops/s | 10.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 486.87K | ± 3.05K | ops/s | **fastest** |
| prometheusWriteToNull | 485.46K | ± 1.61K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.25K | ± 3.07K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.06K | ± 3.59K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48395.726    ± 910.922  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1326.569    ± 106.204  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1205.813     ± 25.807  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1296.466     ± 10.302  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51496.861    ± 217.521  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63777.246   ± 4342.065  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56834.070    ± 376.753  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6180.574     ± 80.600  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6659.846    ± 120.649  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6479.053    ± 179.418  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        671.086     ± 19.608  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.281      ± 5.624  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5749.900   ± 1541.729  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2931.412    ± 259.999  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4569.204     ± 19.628  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474058.241   ± 3591.916  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478250.369   ± 3069.298  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486872.595   ± 3048.004  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485458.207   ± 1609.478  ops/s
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
