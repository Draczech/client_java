# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-21T04:09:10Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.72K | ± 493.03 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.33K | ± 1.03K | ops/s | 1.2x slower |
| prometheusAdd | 51.57K | ± 139.17 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.23K | ± 961.95 | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 172.82 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.47K | ± 224.05 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 202.16 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.41K | ± 151.34 | ops/s | 47x slower |
| openTelemetryAdd | 1.37K | ± 285.66 | ops/s | 49x slower |
| openTelemetryInc | 1.34K | ± 201.95 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.74K | ± 750.04 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 110.73 | ops/s | 1.1x slower |
| prometheusNative | 2.77K | ± 278.16 | ops/s | 1.7x slower |
| openTelemetryClassic | 688.14 | ± 30.58 | ops/s | 6.9x slower |
| openTelemetryExponential | 525.02 | ± 10.34 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.50K | ± 2.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.24K | ± 4.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 472.38K | ± 11.39K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.03K | ± 5.89K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50231.439    ± 961.947  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1373.635    ± 285.660  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1338.408    ± 201.948  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1409.283    ± 151.339  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51571.903    ± 139.172  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66720.292    ± 493.034  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56333.692   ± 1028.469  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6332.184    ± 202.161  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6575.267    ± 172.820  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6471.828    ± 224.048  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        688.137     ± 30.578  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        525.020     ± 10.336  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4743.409    ± 750.036  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2773.646    ± 278.155  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4379.768    ± 110.729  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469027.168   ± 5888.952  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     472379.103  ± 11391.770  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479236.181   ± 4128.617  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484498.175   ± 2360.357  ops/s
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
