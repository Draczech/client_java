# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-05T07:40:51Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.77K | ± 2.04K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.14K | ± 472.05 | ops/s | 1.1x slower |
| prometheusAdd | 47.88K | ± 1.02K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.40K | ± 1.13K | ops/s | 1.4x slower |
| simpleclientInc | 6.34K | ± 50.27 | ops/s | 9.1x slower |
| simpleclientNoLabelsInc | 6.04K | ± 228.59 | ops/s | 9.6x slower |
| simpleclientAdd | 5.62K | ± 311.09 | ops/s | 10x slower |
| openTelemetryAdd | 1.35K | ± 98.69 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.30K | ± 102.26 | ops/s | 44x slower |
| openTelemetryInc | 1.28K | ± 85.79 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.41K | ± 18.91 | ops/s | **fastest** |
| prometheusClassic | 4.35K | ± 583.57 | ops/s | 1.0x slower |
| prometheusNative | 2.87K | ± 239.29 | ops/s | 1.5x slower |
| openTelemetryClassic | 610.48 | ± 16.83 | ops/s | 7.2x slower |
| openTelemetryExponential | 519.44 | ± 22.85 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.62K | ± 1.16K | ops/s | **fastest** |
| prometheusWriteToByteArray | 547.81K | ± 8.49K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.37K | ± 2.78K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 527.79K | ± 3.17K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42398.797   ± 1127.676  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1349.011     ± 98.693  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1275.761     ± 85.794  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1304.969    ± 102.257  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47883.220   ± 1024.852  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57772.694   ± 2036.408  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51144.254    ± 472.047  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5623.817    ± 311.093  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6342.129     ± 50.267  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6044.100    ± 228.590  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        610.480     ± 16.827  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        519.435     ± 22.854  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4351.387    ± 583.572  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2872.448    ± 239.292  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4414.311     ± 18.914  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     527789.368   ± 3172.749  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534374.870   ± 2776.724  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     547812.706   ± 8487.422  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556615.733   ± 1157.487  ops/s
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
