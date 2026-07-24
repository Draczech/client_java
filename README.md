# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-24T06:13:38Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 78.24K | ± 1.63K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.86K | ± 1.14K | ops/s | 1.2x slower |
| prometheusAdd | 63.06K | ± 592.65 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.94K | ± 1.23K | ops/s | 1.4x slower |
| simpleclientInc | 8.16K | ± 35.61 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 7.88K | ± 247.98 | ops/s | 9.9x slower |
| simpleclientAdd | 7.74K | ± 161.07 | ops/s | 10x slower |
| openTelemetryAdd | 1.87K | ± 128.41 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.83K | ± 332.82 | ops/s | 43x slower |
| openTelemetryInc | 1.81K | ± 150.22 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.71K | ± 1.44K | ops/s | **fastest** |
| simpleclient | 5.90K | ± 31.99 | ops/s | 1.3x slower |
| prometheusNative | 3.77K | ± 271.87 | ops/s | 2.0x slower |
| openTelemetryClassic | 790.77 | ± 36.04 | ops/s | 9.7x slower |
| openTelemetryExponential | 681.44 | ± 7.79 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 679.32K | ± 7.77K | ops/s | **fastest** |
| prometheusWriteToByteArray | 660.63K | ± 8.32K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 651.44K | ± 3.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 638.15K | ± 5.96K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56938.381   ± 1231.713  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1872.782    ± 128.408  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1810.903    ± 150.219  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1828.368    ± 332.816  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63057.024    ± 592.646  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      78237.493   ± 1633.780  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66859.923   ± 1135.658  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7737.207    ± 161.069  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8156.887     ± 35.608  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7883.931    ± 247.976  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        790.774     ± 36.035  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        681.440      ± 7.789  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7708.114   ± 1438.731  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3771.106    ± 271.875  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5897.094     ± 31.992  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     638153.022   ± 5959.068  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     651438.407   ± 3364.715  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     660634.033   ± 8317.474  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     679323.358   ± 7770.395  ops/s
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
