# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-10T06:42:24Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.87K | ± 867.59 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.78K | ± 159.43 | ops/s | 1.1x slower |
| prometheusAdd | 48.66K | ± 972.05 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 37.85K | ± 9.64K | ops/s | 1.6x slower |
| simpleclientInc | 6.26K | ± 45.71 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.11K | ± 248.78 | ops/s | 9.6x slower |
| simpleclientAdd | 5.67K | ± 244.04 | ops/s | 10x slower |
| openTelemetryInc | 1.40K | ± 145.88 | ops/s | 42x slower |
| openTelemetryAdd | 1.37K | ± 91.82 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.31K | ± 13.52 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.91K | ± 2.05K | ops/s | **fastest** |
| simpleclient | 4.15K | ± 204.11 | ops/s | 1.7x slower |
| prometheusNative | 2.83K | ± 234.53 | ops/s | 2.4x slower |
| openTelemetryClassic | 608.86 | ± 10.10 | ops/s | 11x slower |
| openTelemetryExponential | 529.97 | ± 15.07 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 535.00K | ± 3.54K | ops/s | **fastest** |
| prometheusWriteToByteArray | 529.61K | ± 2.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 526.48K | ± 3.03K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 510.64K | ± 5.89K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      37851.055   ± 9638.162  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1372.870     ± 91.822  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1404.272    ± 145.878  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1314.909     ± 13.521  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48656.403    ± 972.045  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58867.383    ± 867.587  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51775.557    ± 159.427  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5668.031    ± 244.037  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6257.284     ± 45.715  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6106.691    ± 248.778  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        608.861     ± 10.098  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        529.965     ± 15.072  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6908.389   ± 2054.208  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2831.276    ± 234.531  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4149.987    ± 204.114  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     510644.079   ± 5888.745  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     526479.479   ± 3029.996  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     529609.016   ± 2627.395  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     535000.433   ± 3539.498  ops/s
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
