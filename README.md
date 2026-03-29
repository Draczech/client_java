# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-29T05:43:23Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.42K | ± 128.51 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.31K | ± 1.06K | ops/s | 1.1x slower |
| prometheusAdd | 51.22K | ± 255.70 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.69K | ± 1.48K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.63K | ± 12.46 | ops/s | 9.6x slower |
| simpleclientInc | 6.57K | ± 217.79 | ops/s | 9.7x slower |
| simpleclientAdd | 5.88K | ± 189.11 | ops/s | 11x slower |
| openTelemetryAdd | 1.50K | ± 259.85 | ops/s | 42x slower |
| openTelemetryInc | 1.23K | ± 81.76 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.22K | ± 149.33 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.80K | ± 543.42 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 62.57 | ops/s | 1.1x slower |
| prometheusNative | 3.03K | ± 357.24 | ops/s | 1.6x slower |
| openTelemetryClassic | 683.80 | ± 47.38 | ops/s | 7.0x slower |
| openTelemetryExponential | 562.45 | ± 9.01 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.08K | ± 2.61K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.13K | ± 1.77K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.45K | ± 2.64K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.09K | ± 5.00K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48686.109   ± 1480.532  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1500.539    ± 259.849  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1232.907     ± 81.755  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1222.809    ± 149.327  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51216.735    ± 255.701  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63424.565    ± 128.510  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56313.471   ± 1055.932  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5882.041    ± 189.107  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6566.940    ± 217.788  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6626.737     ± 12.462  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.797     ± 47.379  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.449      ± 9.007  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4797.701    ± 543.420  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3027.799    ± 357.243  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.626     ± 62.573  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481090.992   ± 5002.677  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481452.757   ± 2640.085  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494127.972   ± 1766.556  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495084.553   ± 2606.030  ops/s
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
