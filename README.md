# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-18T07:57:51Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.31K | ± 807.42 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.86K | ± 813.21 | ops/s | 1.2x slower |
| prometheusAdd | 48.18K | ± 380.12 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 42.82K | ± 1.68K | ops/s | 1.4x slower |
| simpleclientInc | 6.31K | ± 48.06 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 5.96K | ± 241.84 | ops/s | 10x slower |
| simpleclientAdd | 5.74K | ± 68.32 | ops/s | 11x slower |
| openTelemetryAdd | 1.48K | ± 144.87 | ops/s | 41x slower |
| openTelemetryInc | 1.46K | ± 112.35 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.40K | ± 46.81 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.92K | ± 1.84K | ops/s | **fastest** |
| simpleclient | 4.53K | ± 47.26 | ops/s | 1.7x slower |
| prometheusNative | 3.03K | ± 240.84 | ops/s | 2.6x slower |
| openTelemetryClassic | 624.24 | ± 15.10 | ops/s | 13x slower |
| openTelemetryExponential | 535.52 | ± 26.93 | ops/s | 15x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 562.55K | ± 3.87K | ops/s | **fastest** |
| prometheusWriteToByteArray | 548.95K | ± 16.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.54K | ± 2.97K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 531.01K | ± 2.52K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42819.623   ± 1684.143  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1482.140    ± 144.868  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1455.539    ± 112.355  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1404.066     ± 46.814  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48183.602    ± 380.118  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60313.560    ± 807.420  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51860.949    ± 813.210  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5743.554     ± 68.321  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6313.599     ± 48.064  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5955.072    ± 241.844  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        624.237     ± 15.097  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        535.517     ± 26.933  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7916.966   ± 1841.852  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3027.858    ± 240.835  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4532.722     ± 47.257  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     531007.332   ± 2523.213  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538540.050   ± 2966.871  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548945.158  ± 16836.654  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     562545.405   ± 3870.806  ops/s
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
