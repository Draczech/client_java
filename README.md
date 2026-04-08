# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-08T05:42:39Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.80K | ± 3.96K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.33K | ± 580.53 | ops/s | 1.1x slower |
| prometheusAdd | 48.47K | ± 223.11 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.73K | ± 260.81 | ops/s | 1.3x slower |
| simpleclientInc | 6.34K | ± 15.69 | ops/s | 9.1x slower |
| simpleclientNoLabelsInc | 6.02K | ± 222.17 | ops/s | 9.6x slower |
| simpleclientAdd | 5.71K | ± 90.87 | ops/s | 10x slower |
| openTelemetryAdd | 1.34K | ± 75.08 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.32K | ± 147.07 | ops/s | 44x slower |
| openTelemetryInc | 1.22K | ± 69.51 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.22K | ± 1.81K | ops/s | **fastest** |
| simpleclient | 4.58K | ± 96.21 | ops/s | 1.4x slower |
| prometheusNative | 2.80K | ± 191.97 | ops/s | 2.2x slower |
| openTelemetryClassic | 631.56 | ± 88.53 | ops/s | 9.8x slower |
| openTelemetryExponential | 524.74 | ± 21.13 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.91K | ± 2.65K | ops/s | **fastest** |
| prometheusWriteToByteArray | 540.82K | ± 8.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 535.54K | ± 3.51K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 522.06K | ± 6.59K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44734.764    ± 260.810  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1336.984     ± 75.077  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1217.034     ± 69.506  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1321.087    ± 147.068  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48470.433    ± 223.107  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57803.524   ± 3961.963  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51326.439    ± 580.527  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5712.714     ± 90.873  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6336.940     ± 15.688  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6015.668    ± 222.174  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        631.563     ± 88.533  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        524.735     ± 21.133  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6216.353   ± 1807.144  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2795.715    ± 191.967  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4584.211     ± 96.207  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     522055.553   ± 6591.403  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     535537.061   ± 3509.960  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     540821.184   ± 8817.862  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555908.566   ± 2648.710  ops/s
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
