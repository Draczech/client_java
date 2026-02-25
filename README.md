# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-25T05:25:12Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.66K | ± 574.34 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.68K | ± 573.29 | ops/s | 1.2x slower |
| prometheusAdd | 51.76K | ± 92.85 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.78K | ± 1.60K | ops/s | 1.3x slower |
| simpleclientInc | 6.65K | ± 199.71 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.48K | ± 146.07 | ops/s | 10x slower |
| simpleclientAdd | 6.26K | ± 227.46 | ops/s | 11x slower |
| openTelemetryAdd | 1.28K | ± 17.47 | ops/s | 52x slower |
| openTelemetryInc | 1.26K | ± 59.12 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.20K | ± 74.55 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.79K | ± 1.32K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 63.37 | ops/s | 1.3x slower |
| prometheusNative | 3.05K | ± 352.90 | ops/s | 1.9x slower |
| openTelemetryClassic | 643.94 | ± 19.60 | ops/s | 9.0x slower |
| openTelemetryExponential | 530.01 | ± 2.06 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.94K | ± 4.00K | ops/s | **fastest** |
| openMetricsWriteToNull | 478.64K | ± 6.23K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 478.15K | ± 4.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.52K | ± 4.33K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49776.441   ± 1603.000  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1284.289     ± 17.473  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1255.626     ± 59.122  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1203.030     ± 74.547  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51756.072     ± 92.855  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66660.898    ± 574.339  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56676.451    ± 573.293  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6256.891    ± 227.462  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6653.397    ± 199.714  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6483.000    ± 146.072  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        643.936     ± 19.601  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        530.013      ± 2.059  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5789.578   ± 1315.576  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3049.327    ± 352.902  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4562.140     ± 63.371  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473523.483   ± 4330.425  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478636.206   ± 6228.598  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     478154.828   ± 4474.345  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492939.746   ± 4002.737  ops/s
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
