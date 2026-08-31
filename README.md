# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-31T09:03:20Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.16K | ± 493.95 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.23K | ± 1.45K | ops/s | 1.2x slower |
| prometheusAdd | 51.41K | ± 167.69 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.40K | ± 1.23K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.62K | ± 17.12 | ops/s | 10x slower |
| simpleclientInc | 6.60K | ± 186.34 | ops/s | 10x slower |
| simpleclientAdd | 6.22K | ± 331.47 | ops/s | 11x slower |
| openTelemetryAdd | 1.64K | ± 352.47 | ops/s | 40x slower |
| openTelemetryInc | 1.37K | ± 139.44 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.32K | ± 200.38 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.76K | ± 1.18K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 73.15 | ops/s | 1.1x slower |
| prometheusNative | 2.95K | ± 253.44 | ops/s | 1.6x slower |
| openTelemetryClassic | 672.60 | ± 19.60 | ops/s | 7.1x slower |
| openTelemetryExponential | 554.75 | ± 35.31 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 482.20K | ± 5.84K | ops/s | **fastest** |
| prometheusWriteToNull | 481.55K | ± 6.75K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.62K | ± 3.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 467.54K | ± 10.12K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49403.411   ± 1233.725  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1640.646    ± 352.468  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1369.508    ± 139.440  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1321.694    ± 200.376  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51410.714    ± 167.693  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66164.589    ± 493.949  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56226.236   ± 1450.197  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6215.206    ± 331.474  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6601.037    ± 186.341  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6615.868     ± 17.121  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        672.605     ± 19.600  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.751     ± 35.313  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4762.022   ± 1177.069  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2951.532    ± 253.439  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4442.463     ± 73.152  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469624.313   ± 3791.656  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     467537.644  ± 10118.390  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482198.921   ± 5844.684  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481546.872   ± 6748.387  ops/s
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
