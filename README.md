# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-04T05:22:03Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.54K | ± 1.72K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.96K | ± 894.78 | ops/s | 1.2x slower |
| prometheusAdd | 51.29K | ± 210.64 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.18K | ± 1.63K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.53K | ± 141.77 | ops/s | 10x slower |
| simpleclientInc | 6.46K | ± 68.37 | ops/s | 10x slower |
| simpleclientAdd | 6.22K | ± 250.06 | ops/s | 11x slower |
| openTelemetryAdd | 1.43K | ± 227.20 | ops/s | 46x slower |
| openTelemetryInc | 1.35K | ± 116.12 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.22K | ± 43.86 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.99K | ± 1.12K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 52.00 | ops/s | 1.3x slower |
| prometheusNative | 2.61K | ± 91.06 | ops/s | 2.3x slower |
| openTelemetryClassic | 697.15 | ± 39.27 | ops/s | 8.6x slower |
| openTelemetryExponential | 553.99 | ± 21.37 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.34K | ± 2.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.37K | ± 3.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.58K | ± 5.34K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.71K | ± 4.26K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48179.389   ± 1632.049  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1434.960    ± 227.201  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1352.427    ± 116.121  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1222.802     ± 43.860  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51287.502    ± 210.637  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65538.468   ± 1720.229  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56964.457    ± 894.776  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6221.257    ± 250.063  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6455.473     ± 68.372  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6529.388    ± 141.773  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        697.146     ± 39.269  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        553.986     ± 21.367  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5992.177   ± 1123.166  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2613.521     ± 91.060  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4459.768     ± 51.999  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470709.441   ± 4257.285  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476580.104   ± 5339.816  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485373.302   ± 3075.397  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493335.602   ± 2937.434  ops/s
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
