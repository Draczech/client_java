# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-04T06:38:58Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 30.89K | ± 165.55 | ops/s | **fastest** |
| prometheusInc | 30.35K | ± 981.43 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 30.15K | ± 1.61K | ops/s | 1.0x slower |
| prometheusAdd | 28.47K | ± 10.38 | ops/s | 1.1x slower |
| simpleclientInc | 6.94K | ± 98.14 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.56K | ± 103.05 | ops/s | 4.7x slower |
| simpleclientAdd | 6.47K | ± 194.62 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.50K | ± 71.26 | ops/s | 21x slower |
| openTelemetryInc | 1.41K | ± 22.12 | ops/s | 22x slower |
| openTelemetryAdd | 1.38K | ± 26.82 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.46K | ± 80.58 | ops/s | **fastest** |
| prometheusClassic | 3.38K | ± 231.21 | ops/s | 1.3x slower |
| prometheusNative | 2.18K | ± 156.46 | ops/s | 2.0x slower |
| openTelemetryClassic | 506.34 | ± 12.72 | ops/s | 8.8x slower |
| openTelemetryExponential | 425.65 | ± 15.06 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 318.29K | ± 3.07K | ops/s | **fastest** |
| prometheusWriteToByteArray | 316.68K | ± 1.09K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 298.47K | ± 3.19K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 297.83K | ± 1.87K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30153.751   ± 1607.749  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1384.197     ± 26.817  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1405.533     ± 22.124  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1499.602     ± 71.263  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28471.307     ± 10.378  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30347.849    ± 981.429  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30887.491    ± 165.548  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6470.294    ± 194.620  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6936.358     ± 98.140  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6557.043    ± 103.052  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        506.338     ± 12.724  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        425.646     ± 15.062  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3382.648    ± 231.212  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2183.070    ± 156.460  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4461.696     ± 80.579  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297827.047   ± 1869.989  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     298473.462   ± 3194.503  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     316676.028   ± 1090.839  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     318289.827   ± 3066.312  ops/s
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
