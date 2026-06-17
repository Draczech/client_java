# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-17T08:13:16Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.61K | ± 791.73 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.03K | ± 1.02K | ops/s | 1.2x slower |
| prometheusAdd | 51.48K | ± 205.57 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.68K | ± 2.03K | ops/s | 1.4x slower |
| simpleclientInc | 6.70K | ± 8.58 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.35K | ± 227.85 | ops/s | 10x slower |
| simpleclientAdd | 6.29K | ± 303.33 | ops/s | 11x slower |
| openTelemetryAdd | 1.69K | ± 351.86 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.24K | ± 27.04 | ops/s | 54x slower |
| openTelemetryInc | 1.21K | ± 15.35 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 1.58K | ops/s | **fastest** |
| simpleclient | 4.30K | ± 121.60 | ops/s | 1.2x slower |
| prometheusNative | 3.16K | ± 120.39 | ops/s | 1.7x slower |
| openTelemetryClassic | 682.35 | ± 35.72 | ops/s | 7.7x slower |
| openTelemetryExponential | 572.36 | ± 60.00 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 475.78K | ± 5.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 474.87K | ± 3.67K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.33K | ± 5.97K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 468.47K | ± 6.72K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48676.329   ± 2033.254  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1687.490    ± 351.862  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1211.444     ± 15.354  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1235.615     ± 27.039  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51475.737    ± 205.569  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66613.362    ± 791.728  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56029.465   ± 1021.091  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6286.939    ± 303.328  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6699.150      ± 8.580  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6350.250    ± 227.850  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.348     ± 35.716  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        572.356     ± 60.003  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5262.751   ± 1579.524  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3160.925    ± 120.386  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4303.493    ± 121.604  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470332.791   ± 5972.957  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468468.046   ± 6722.712  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     474871.617   ± 3673.397  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     475782.284   ± 5580.146  ops/s
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
