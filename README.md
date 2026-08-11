# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-11T04:40:55Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.29K | ± 329.87 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.45K | ± 1.10K | ops/s | 1.2x slower |
| prometheusAdd | 50.41K | ± 504.90 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.00K | ± 392.79 | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 69.35 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.52K | ± 139.45 | ops/s | 10x slower |
| simpleclientAdd | 6.44K | ± 38.25 | ops/s | 10x slower |
| openTelemetryAdd | 1.46K | ± 222.01 | ops/s | 45x slower |
| openTelemetryInc | 1.34K | ± 123.35 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.29K | ± 243.35 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.64K | ± 900.55 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 54.11 | ops/s | 1.3x slower |
| prometheusNative | 2.90K | ± 322.31 | ops/s | 1.9x slower |
| openTelemetryClassic | 652.09 | ± 20.70 | ops/s | 8.6x slower |
| openTelemetryExponential | 557.73 | ± 41.30 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.86K | ± 6.62K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.47K | ± 1.95K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.67K | ± 4.15K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.16K | ± 5.99K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50004.073    ± 392.795  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1459.130    ± 222.006  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1338.910    ± 123.352  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1292.818    ± 243.348  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50412.160    ± 504.904  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66286.051    ± 329.868  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56449.767   ± 1098.968  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6444.679     ± 38.254  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6660.982     ± 69.348  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6515.547    ± 139.451  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        652.092     ± 20.703  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.732     ± 41.300  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5636.110    ± 900.555  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2902.396    ± 322.307  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4468.690     ± 54.112  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477160.754   ± 5988.308  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482665.370   ± 4151.728  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487466.024   ± 1953.963  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494864.069   ± 6616.246  ops/s
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
