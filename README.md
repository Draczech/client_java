# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-16T05:46:15Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.43K | ± 1.45K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.48K | ± 1.19K | ops/s | 1.2x slower |
| prometheusAdd | 50.53K | ± 322.89 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.72K | ± 659.59 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.58K | ± 184.81 | ops/s | 9.9x slower |
| simpleclientInc | 6.56K | ± 189.00 | ops/s | 10.0x slower |
| simpleclientAdd | 6.41K | ± 250.31 | ops/s | 10x slower |
| openTelemetryAdd | 1.61K | ± 254.92 | ops/s | 41x slower |
| openTelemetryInc | 1.38K | ± 187.81 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.34K | ± 77.08 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.70K | ± 628.78 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 18.20 | ops/s | 1.0x slower |
| prometheusNative | 2.83K | ± 286.91 | ops/s | 1.7x slower |
| openTelemetryClassic | 685.20 | ± 21.07 | ops/s | 6.9x slower |
| openTelemetryExponential | 571.11 | ± 15.54 | ops/s | 8.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.67K | ± 2.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.63K | ± 2.16K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.50K | ± 1.74K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.48K | ± 5.50K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48722.185    ± 659.593  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1605.169    ± 254.919  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1375.262    ± 187.811  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1343.022     ± 77.078  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50529.066    ± 322.890  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65433.055   ± 1453.644  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56477.805   ± 1185.278  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6412.312    ± 250.315  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6558.543    ± 189.003  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6582.159    ± 184.808  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        685.198     ± 21.069  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        571.112     ± 15.539  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4697.886    ± 628.784  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2829.961    ± 286.911  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4559.717     ± 18.204  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477497.288   ± 1738.760  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476479.945   ± 5500.376  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488633.092   ± 2159.614  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488666.840   ± 2490.475  ops/s
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
