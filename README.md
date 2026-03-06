# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-06T05:15:29Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.52K | ± 716.68 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.03K | ± 475.23 | ops/s | 1.2x slower |
| prometheusAdd | 51.27K | ± 411.78 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.42K | ± 1.15K | ops/s | 1.4x slower |
| simpleclientInc | 6.68K | ± 118.36 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.43K | ± 217.94 | ops/s | 10x slower |
| simpleclientAdd | 6.43K | ± 206.79 | ops/s | 10x slower |
| openTelemetryAdd | 1.46K | ± 213.98 | ops/s | 45x slower |
| openTelemetryInc | 1.38K | ± 147.17 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.31K | ± 184.82 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.88K | ± 672.98 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 59.15 | ops/s | 1.3x slower |
| prometheusNative | 2.62K | ± 144.23 | ops/s | 2.2x slower |
| openTelemetryClassic | 695.96 | ± 5.56 | ops/s | 8.4x slower |
| openTelemetryExponential | 546.09 | ± 19.53 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.84K | ± 990.76 | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.43K | ± 1.03K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 484.75K | ± 1.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.20K | ± 8.19K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48424.231   ± 1147.765  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1463.910    ± 213.977  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1383.495    ± 147.174  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1313.905    ± 184.816  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51273.172    ± 411.784  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66519.431    ± 716.682  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57027.817    ± 475.233  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6428.553    ± 206.788  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6675.467    ± 118.359  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6433.892    ± 217.935  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        695.961      ± 5.559  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.090     ± 19.531  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5879.168    ± 672.984  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2615.543    ± 144.230  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4562.214     ± 59.146  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474197.858   ± 8190.322  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484753.536   ± 1503.738  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489430.713   ± 1028.883  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491843.319    ± 990.759  ops/s
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
