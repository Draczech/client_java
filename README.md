# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-28T07:21:28Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 73.79K | ± 2.18K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.76K | ± 155.30 | ops/s | 1.1x slower |
| prometheusAdd | 62.80K | ± 396.63 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.63K | ± 241.43 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 8.05K | ± 128.65 | ops/s | 9.2x slower |
| simpleclientInc | 8.01K | ± 174.08 | ops/s | 9.2x slower |
| simpleclientAdd | 7.85K | ± 209.12 | ops/s | 9.4x slower |
| openTelemetryIncNoLabels | 2.23K | ± 365.11 | ops/s | 33x slower |
| openTelemetryInc | 1.96K | ± 386.27 | ops/s | 38x slower |
| openTelemetryAdd | 1.65K | ± 5.08 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.61K | ± 1.55K | ops/s | **fastest** |
| simpleclient | 5.55K | ± 175.65 | ops/s | 1.4x slower |
| prometheusNative | 3.89K | ± 273.34 | ops/s | 2.0x slower |
| openTelemetryClassic | 780.10 | ± 22.60 | ops/s | 9.8x slower |
| openTelemetryExponential | 664.31 | ± 19.30 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 666.18K | ± 12.09K | ops/s | **fastest** |
| prometheusWriteToByteArray | 656.31K | ± 4.86K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 639.75K | ± 8.46K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 631.21K | ± 5.64K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56631.888    ± 241.430  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1651.615      ± 5.076  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1959.361    ± 386.268  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2226.265    ± 365.112  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62797.386    ± 396.629  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      73794.423   ± 2180.439  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66760.702    ± 155.301  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7854.316    ± 209.121  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8012.229    ± 174.085  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8051.077    ± 128.650  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        780.102     ± 22.601  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        664.314     ± 19.299  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7614.685   ± 1554.206  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3893.873    ± 273.344  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5552.550    ± 175.654  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     631213.856   ± 5636.837  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     639748.307   ± 8456.095  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     656310.988   ± 4863.546  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     666182.202  ± 12088.184  ops/s
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
