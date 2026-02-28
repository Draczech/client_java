# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-28T05:01:40Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.55K | ± 60.26 | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.80K | ± 1.06K | ops/s | 1.1x slower |
| codahaleIncNoLabels | 28.69K | ± 577.82 | ops/s | 1.1x slower |
| prometheusAdd | 28.45K | ± 121.34 | ops/s | 1.1x slower |
| simpleclientInc | 7.02K | ± 61.48 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.82K | ± 260.79 | ops/s | 4.6x slower |
| simpleclientAdd | 6.76K | ± 85.90 | ops/s | 4.7x slower |
| openTelemetryIncNoLabels | 1.49K | ± 66.64 | ops/s | 21x slower |
| openTelemetryInc | 1.38K | ± 81.22 | ops/s | 23x slower |
| openTelemetryAdd | 1.36K | ± 63.56 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.58K | ± 62.29 | ops/s | **fastest** |
| prometheusClassic | 2.87K | ± 93.22 | ops/s | 1.6x slower |
| prometheusNative | 2.47K | ± 167.55 | ops/s | 1.9x slower |
| openTelemetryClassic | 497.97 | ± 7.28 | ops/s | 9.2x slower |
| openTelemetryExponential | 400.51 | ± 27.77 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 306.22K | ± 2.55K | ops/s | **fastest** |
| prometheusWriteToByteArray | 306.15K | ± 1.91K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 289.38K | ± 2.20K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 288.56K | ± 1.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28685.463    ± 577.825  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1362.595     ± 63.564  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1376.440     ± 81.216  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1493.374     ± 66.635  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28449.393    ± 121.339  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31550.746     ± 60.264  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29795.103   ± 1058.640  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6763.726     ± 85.900  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7016.643     ± 61.477  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6818.411    ± 260.786  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        497.968      ± 7.278  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        400.508     ± 27.771  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2871.009     ± 93.225  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2468.552    ± 167.549  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4581.130     ± 62.295  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     289379.179   ± 2203.917  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     288557.129   ± 1551.547  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     306152.293   ± 1910.225  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     306220.416   ± 2554.883  ops/s
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
