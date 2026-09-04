# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-04T07:54:15Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.50K | ± 1.61K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 257.64 | ops/s | 1.2x slower |
| prometheusAdd | 50.86K | ± 298.40 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.26K | ± 1.54K | ops/s | 1.4x slower |
| simpleclientInc | 6.63K | ± 98.63 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.26K | ± 84.23 | ops/s | 10x slower |
| simpleclientAdd | 6.24K | ± 342.94 | ops/s | 11x slower |
| openTelemetryInc | 1.38K | ± 186.65 | ops/s | 47x slower |
| openTelemetryAdd | 1.38K | ± 227.28 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.19K | ± 1.73 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.36K | ± 1.26K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 55.79 | ops/s | 1.4x slower |
| prometheusNative | 2.96K | ± 334.69 | ops/s | 2.1x slower |
| openTelemetryClassic | 709.46 | ± 24.59 | ops/s | 9.0x slower |
| openTelemetryExponential | 562.12 | ± 13.05 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 481.65K | ± 7.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 466.53K | ± 5.52K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 460.79K | ± 5.57K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 457.39K | ± 8.75K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48263.149   ± 1541.529  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1377.207    ± 227.278  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1379.159    ± 186.650  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1191.375      ± 1.733  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50857.598    ± 298.402  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65501.650   ± 1605.476  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56833.550    ± 257.641  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6237.744    ± 342.937  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6625.150     ± 98.629  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6261.924     ± 84.227  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        709.462     ± 24.590  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.118     ± 13.054  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6359.403   ± 1255.573  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2959.411    ± 334.692  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4444.809     ± 55.793  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     457392.878   ± 8753.765  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     460785.424   ± 5568.536  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     466530.555   ± 5523.706  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481652.424   ± 7347.775  ops/s
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
