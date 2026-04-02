# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-02T05:33:32Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.56K | ± 25.93 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.64K | ± 304.29 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.07K | ± 734.66 | ops/s | 1.1x slower |
| prometheusAdd | 27.38K | ± 1.70K | ops/s | 1.2x slower |
| simpleclientInc | 6.87K | ± 201.12 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.77K | ± 135.34 | ops/s | 4.7x slower |
| simpleclientAdd | 6.42K | ± 272.22 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 1.48K | ± 231.59 | ops/s | 21x slower |
| openTelemetryAdd | 1.46K | ± 62.24 | ops/s | 22x slower |
| openTelemetryInc | 1.29K | ± 74.18 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.49K | ± 113.12 | ops/s | **fastest** |
| prometheusClassic | 2.63K | ± 166.85 | ops/s | 1.7x slower |
| prometheusNative | 2.11K | ± 163.77 | ops/s | 2.1x slower |
| openTelemetryClassic | 531.59 | ± 10.18 | ops/s | 8.4x slower |
| openTelemetryExponential | 439.41 | ± 13.74 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 311.22K | ± 3.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 308.66K | ± 3.18K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 291.56K | ± 2.39K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 287.75K | ± 1.44K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29069.063    ± 734.659  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1455.464     ± 62.241  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1293.866     ± 74.181  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1479.508    ± 231.595  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27377.647   ± 1701.997  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31563.715     ± 25.926  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30640.118    ± 304.291  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6422.354    ± 272.221  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6866.272    ± 201.120  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6768.564    ± 135.342  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        531.595     ± 10.176  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        439.410     ± 13.740  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2630.841    ± 166.849  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2112.406    ± 163.774  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4486.996    ± 113.119  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     287752.331   ± 1442.274  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     291555.849   ± 2389.652  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     308662.070   ± 3179.921  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     311218.477   ± 3864.231  ops/s
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
