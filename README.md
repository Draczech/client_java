# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-02T06:30:11Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.53K | ± 654.14 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.27K | ± 588.26 | ops/s | 1.2x slower |
| prometheusAdd | 51.20K | ± 351.02 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.86K | ± 1.86K | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 54.09 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.38K | ± 208.59 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 163.95 | ops/s | 11x slower |
| openTelemetryAdd | 1.55K | ± 273.37 | ops/s | 43x slower |
| openTelemetryInc | 1.48K | ± 204.68 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.35K | ± 246.07 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 1.34K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 39.17 | ops/s | 1.2x slower |
| prometheusNative | 3.03K | ± 397.04 | ops/s | 1.8x slower |
| openTelemetryClassic | 675.66 | ± 14.94 | ops/s | 7.9x slower |
| openTelemetryExponential | 527.96 | ± 6.82 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.08K | ± 2.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 480.29K | ± 4.58K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.28K | ± 5.20K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 469.60K | ± 6.21K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48861.913   ± 1859.234  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1554.385    ± 273.368  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1475.517    ± 204.677  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1349.713    ± 246.069  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51203.342    ± 351.020  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66528.088    ± 654.145  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56272.878    ± 588.262  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6315.720    ± 163.953  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6655.904     ± 54.091  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6382.753    ± 208.586  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        675.660     ± 14.942  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        527.959      ± 6.820  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5359.741   ± 1343.978  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3029.409    ± 397.040  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4470.063     ± 39.175  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471276.164   ± 5200.393  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     469601.302   ± 6213.250  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480291.916   ± 4581.347  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485078.493   ± 2888.736  ops/s
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
