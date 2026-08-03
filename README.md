# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-03T06:42:54Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.57K | ± 783.39 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.75K | ± 455.70 | ops/s | 1.2x slower |
| prometheusAdd | 51.05K | ± 708.93 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.79K | ± 1.36K | ops/s | 1.4x slower |
| simpleclientInc | 6.65K | ± 44.11 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.42K | ± 94.90 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 292.09 | ops/s | 10x slower |
| openTelemetryAdd | 1.60K | ± 328.73 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.45K | ± 165.94 | ops/s | 45x slower |
| openTelemetryInc | 1.37K | ± 150.05 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 1.41K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 54.91 | ops/s | 1.2x slower |
| prometheusNative | 2.79K | ± 131.99 | ops/s | 1.9x slower |
| openTelemetryClassic | 694.71 | ± 20.94 | ops/s | 7.6x slower |
| openTelemetryExponential | 566.75 | ± 22.84 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.47K | ± 3.64K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.95K | ± 1.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.14K | ± 2.98K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.99K | ± 2.04K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47790.333   ± 1364.955  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1598.626    ± 328.732  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1365.687    ± 150.045  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1453.912    ± 165.943  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51050.306    ± 708.934  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65572.232    ± 783.393  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56748.092    ± 455.703  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6316.006    ± 292.085  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6647.380     ± 44.112  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6422.222     ± 94.900  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        694.712     ± 20.937  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.747     ± 22.837  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5251.872   ± 1412.510  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2786.130    ± 131.987  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4421.044     ± 54.909  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472986.396   ± 2043.100  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481142.911   ± 2979.297  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487949.829   ± 1878.637  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492472.111   ± 3644.416  ops/s
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
