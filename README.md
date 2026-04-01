# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-01T05:54:24Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.36K | ± 274.78 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.57K | ± 1.17K | ops/s | 1.2x slower |
| prometheusAdd | 51.30K | ± 395.81 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.45K | ± 2.05K | ops/s | 1.4x slower |
| simpleclientInc | 6.67K | ± 51.91 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.49K | ± 183.51 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 246.73 | ops/s | 11x slower |
| openTelemetryInc | 1.41K | ± 259.91 | ops/s | 47x slower |
| openTelemetryAdd | 1.29K | ± 36.59 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.19K | ± 42.23 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.06K | ± 1.34K | ops/s | **fastest** |
| simpleclient | 4.37K | ± 61.23 | ops/s | 1.4x slower |
| prometheusNative | 3.03K | ± 315.58 | ops/s | 2.0x slower |
| openTelemetryClassic | 657.52 | ± 14.26 | ops/s | 9.2x slower |
| openTelemetryExponential | 545.69 | ± 29.20 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.91K | ± 4.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.00K | ± 1.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.42K | ± 3.90K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 480.50K | ± 4.85K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48445.222   ± 2045.609  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1287.223     ± 36.595  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1410.984    ± 259.913  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1191.842     ± 42.225  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51303.992    ± 395.810  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66360.590    ± 274.782  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56573.329   ± 1171.218  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6313.390    ± 246.732  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6665.863     ± 51.911  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6492.409    ± 183.509  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        657.518     ± 14.263  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.690     ± 29.197  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6056.682   ± 1339.477  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3033.424    ± 315.583  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4370.231     ± 61.229  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     480502.076   ± 4852.360  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483420.374   ± 3904.145  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490999.191   ± 1274.851  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494905.790   ± 4151.708  ops/s
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
