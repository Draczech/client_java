# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-27T05:18:03Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.59K | ± 43.40 | ops/s | **fastest** |
| codahaleIncNoLabels | 30.50K | ± 1.11K | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 30.49K | ± 1.50K | ops/s | 1.0x slower |
| prometheusAdd | 28.52K | ± 18.96 | ops/s | 1.1x slower |
| simpleclientInc | 7.16K | ± 60.37 | ops/s | 4.4x slower |
| simpleclientNoLabelsInc | 6.81K | ± 208.55 | ops/s | 4.6x slower |
| simpleclientAdd | 6.66K | ± 207.72 | ops/s | 4.7x slower |
| openTelemetryIncNoLabels | 1.34K | ± 52.41 | ops/s | 24x slower |
| openTelemetryInc | 1.32K | ± 53.90 | ops/s | 24x slower |
| openTelemetryAdd | 1.30K | ± 23.15 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.53K | ± 82.10 | ops/s | **fastest** |
| prometheusClassic | 2.91K | ± 265.57 | ops/s | 1.6x slower |
| prometheusNative | 2.28K | ± 46.00 | ops/s | 2.0x slower |
| openTelemetryClassic | 499.49 | ± 9.90 | ops/s | 9.1x slower |
| openTelemetryExponential | 378.79 | ± 13.95 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 314.92K | ± 3.59K | ops/s | **fastest** |
| prometheusWriteToByteArray | 310.15K | ± 5.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 294.46K | ± 4.65K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 291.67K | ± 2.79K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30503.896   ± 1109.054  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1303.234     ± 23.155  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1318.050     ± 53.897  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1342.510     ± 52.414  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28521.619     ± 18.959  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31585.654     ± 43.399  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30492.024   ± 1496.825  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6655.833    ± 207.718  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7159.388     ± 60.368  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6805.753    ± 208.549  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        499.486      ± 9.896  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        378.792     ± 13.954  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2907.598    ± 265.566  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2278.991     ± 46.005  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4529.683     ± 82.095  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     291670.088   ± 2794.476  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     294456.485   ± 4653.289  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     310154.097   ± 5127.728  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     314917.999   ± 3594.437  ops/s
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
