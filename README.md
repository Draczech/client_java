# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-15T05:39:07Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.30K | ± 2.04K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.67K | ± 408.94 | ops/s | 1.2x slower |
| prometheusAdd | 51.01K | ± 579.52 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.94K | ± 575.39 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.60K | ± 127.21 | ops/s | 9.9x slower |
| simpleclientInc | 6.57K | ± 177.60 | ops/s | 9.9x slower |
| simpleclientAdd | 6.06K | ± 160.95 | ops/s | 11x slower |
| openTelemetryInc | 1.41K | ± 176.24 | ops/s | 46x slower |
| openTelemetryAdd | 1.37K | ± 148.21 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.31K | ± 154.50 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.55K | ± 30.52 | ops/s | **fastest** |
| prometheusClassic | 4.17K | ± 89.02 | ops/s | 1.1x slower |
| prometheusNative | 2.83K | ± 353.28 | ops/s | 1.6x slower |
| openTelemetryClassic | 674.34 | ± 30.44 | ops/s | 6.7x slower |
| openTelemetryExponential | 537.30 | ± 6.05 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.76K | ± 2.13K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.98K | ± 2.25K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.40K | ± 2.37K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.20K | ± 5.23K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50940.640    ± 575.387  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1367.977    ± 148.215  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1408.267    ± 176.235  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1308.250    ± 154.497  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51005.863    ± 579.519  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65303.826   ± 2039.569  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56673.034    ± 408.935  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6062.571    ± 160.949  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6574.539    ± 177.600  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6602.234    ± 127.214  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        674.337     ± 30.438  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        537.299      ± 6.049  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4173.771     ± 89.016  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2833.524    ± 353.282  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4545.951     ± 30.516  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483395.981   ± 2366.759  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483195.522   ± 5232.896  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490981.831   ± 2254.019  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494763.472   ± 2131.700  ops/s
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
