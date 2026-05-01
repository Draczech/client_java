# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-01T06:48:22Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.17K | ± 1.78K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.39K | ± 1.04K | ops/s | 1.1x slower |
| prometheusAdd | 51.49K | ± 273.96 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.43K | ± 1.30K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 165.44 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.30K | ± 71.91 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 187.15 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 160.98 | ops/s | 45x slower |
| openTelemetryInc | 1.24K | ± 76.84 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.18K | ± 40.62 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.65K | ± 2.43K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 63.60 | ops/s | 1.3x slower |
| prometheusNative | 2.97K | ± 367.52 | ops/s | 1.9x slower |
| openTelemetryClassic | 682.28 | ± 27.66 | ops/s | 8.3x slower |
| openTelemetryExponential | 532.73 | ± 29.20 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 492.88K | ± 2.48K | ops/s | **fastest** |
| openMetricsWriteToNull | 489.80K | ± 952.98 | ops/s | 1.0x slower |
| prometheusWriteToNull | 489.29K | ± 5.57K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.65K | ± 1.19K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49431.107   ± 1298.588  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1428.413    ± 160.976  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1242.968     ± 76.841  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1184.269     ± 40.624  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51486.318    ± 273.962  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64170.676   ± 1782.759  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56392.647   ± 1037.016  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6295.650    ± 187.147  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6549.037    ± 165.440  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6300.458     ± 71.910  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.283     ± 27.663  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        532.726     ± 29.196  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5645.501   ± 2426.764  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2968.363    ± 367.517  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4463.260     ± 63.605  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483651.938   ± 1188.072  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489798.645    ± 952.981  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492881.848   ± 2482.783  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489288.870   ± 5573.010  ops/s
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
