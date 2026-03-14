# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-14T05:16:12Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.15K | ± 312.13 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.76K | ± 339.10 | ops/s | 1.2x slower |
| prometheusAdd | 50.72K | ± 544.94 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.43K | ± 901.62 | ops/s | 1.4x slower |
| simpleclientInc | 6.77K | ± 25.69 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.70K | ± 16.18 | ops/s | 9.9x slower |
| simpleclientAdd | 6.40K | ± 255.81 | ops/s | 10x slower |
| openTelemetryAdd | 1.42K | ± 194.47 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.29K | ± 22.88 | ops/s | 51x slower |
| openTelemetryInc | 1.25K | ± 38.74 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 1.47K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 47.14 | ops/s | 1.2x slower |
| prometheusNative | 3.20K | ± 167.07 | ops/s | 1.6x slower |
| openTelemetryClassic | 662.46 | ± 23.86 | ops/s | 7.9x slower |
| openTelemetryExponential | 525.69 | ± 16.78 | ops/s | 10.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 481.68K | ± 2.67K | ops/s | **fastest** |
| prometheusWriteToNull | 481.04K | ± 5.95K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 467.65K | ± 4.19K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.96K | ± 4.76K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48427.859    ± 901.622  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1423.264    ± 194.474  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1247.801     ± 38.744  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1286.866     ± 22.876  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50724.909    ± 544.937  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66150.263    ± 312.132  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56759.901    ± 339.097  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6399.423    ± 255.806  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6773.078     ± 25.691  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6697.939     ± 16.185  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        662.462     ± 23.856  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        525.685     ± 16.775  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5235.622   ± 1468.772  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3201.149    ± 167.072  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4549.450     ± 47.137  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464964.301   ± 4758.698  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     467650.438   ± 4194.199  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481683.332   ± 2667.017  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481041.514   ± 5950.292  ops/s
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
