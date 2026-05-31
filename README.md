# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-31T07:23:01Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.00K | ± 1.32K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.55K | ± 503.99 | ops/s | 1.1x slower |
| prometheusAdd | 50.64K | ± 472.14 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.36K | ± 1.39K | ops/s | 1.3x slower |
| simpleclientInc | 6.69K | ± 18.78 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.31K | ± 243.31 | ops/s | 10x slower |
| simpleclientAdd | 5.95K | ± 153.11 | ops/s | 11x slower |
| openTelemetryInc | 1.30K | ± 21.54 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.30K | ± 167.99 | ops/s | 50x slower |
| openTelemetryAdd | 1.25K | ± 26.26 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.70K | ± 575.47 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 39.84 | ops/s | 1.1x slower |
| prometheusNative | 3.17K | ± 65.38 | ops/s | 1.5x slower |
| openTelemetryClassic | 711.79 | ± 27.27 | ops/s | 6.6x slower |
| openTelemetryExponential | 556.83 | ± 8.09 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 476.72K | ± 4.81K | ops/s | **fastest** |
| openMetricsWriteToNull | 471.50K | ± 4.61K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 470.46K | ± 6.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 460.06K | ± 3.06K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48357.526   ± 1394.767  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1250.402     ± 26.258  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1298.578     ± 21.539  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1298.560    ± 167.987  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50642.222    ± 472.139  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64998.730   ± 1324.244  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56553.324    ± 503.988  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5945.330    ± 153.110  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6687.578     ± 18.783  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6308.284    ± 243.309  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        711.791     ± 27.269  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.828      ± 8.093  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4698.994    ± 575.472  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3167.039     ± 65.381  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4460.545     ± 39.843  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     460064.267   ± 3055.514  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471503.132   ± 4609.656  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     470461.724   ± 6937.348  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     476716.198   ± 4810.758  ops/s
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
