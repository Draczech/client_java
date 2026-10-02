# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-02T08:54:49Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.23K | ± 1.49K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.98K | ± 418.44 | ops/s | 1.1x slower |
| prometheusAdd | 51.42K | ± 166.28 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.36K | ± 1.43K | ops/s | 1.3x slower |
| simpleclientInc | 6.39K | ± 164.72 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.25K | ± 6.94 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 214.74 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.31K | ± 148.22 | ops/s | 50x slower |
| openTelemetryAdd | 1.26K | ± 27.33 | ops/s | 52x slower |
| openTelemetryInc | 1.25K | ± 9.43 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.45K | ± 1.38K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 60.86 | ops/s | 1.7x slower |
| prometheusNative | 2.73K | ± 342.78 | ops/s | 2.7x slower |
| openTelemetryClassic | 710.60 | ± 29.80 | ops/s | 10x slower |
| openTelemetryExponential | 579.65 | ± 51.43 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.35K | ± 2.34K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.45K | ± 995.29 | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.30K | ± 7.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.00K | ± 9.71K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48363.772   ± 1431.238  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1256.226     ± 27.333  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1246.907      ± 9.428  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1313.418    ± 148.217  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51424.509    ± 166.278  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65233.814   ± 1489.369  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56979.129    ± 418.437  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6186.717    ± 214.741  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6391.828    ± 164.719  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6251.825      ± 6.939  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        710.605     ± 29.804  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        579.645     ± 51.431  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7453.202   ± 1379.313  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2732.435    ± 342.785  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4458.305     ± 60.855  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467003.674   ± 9710.580  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481301.614   ± 7883.388  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487445.099    ± 995.295  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488350.806   ± 2337.664  ops/s
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
