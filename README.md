# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-07T05:06:26Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.85K | ± 1.76K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.72K | ± 213.11 | ops/s | 1.2x slower |
| prometheusAdd | 50.78K | ± 727.46 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.21K | ± 1.59K | ops/s | 1.4x slower |
| simpleclientInc | 6.76K | ± 31.14 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.45K | ± 189.05 | ops/s | 10x slower |
| simpleclientAdd | 6.43K | ± 204.95 | ops/s | 10x slower |
| openTelemetryAdd | 1.58K | ± 293.85 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.32K | ± 186.09 | ops/s | 50x slower |
| openTelemetryInc | 1.28K | ± 42.02 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.69K | ± 848.15 | ops/s | **fastest** |
| simpleclient | 4.51K | ± 18.13 | ops/s | 1.5x slower |
| prometheusNative | 3.03K | ± 380.59 | ops/s | 2.2x slower |
| openTelemetryClassic | 712.87 | ± 26.69 | ops/s | 9.4x slower |
| openTelemetryExponential | 580.43 | ± 24.03 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.83K | ± 3.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.76K | ± 4.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.63K | ± 3.65K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.31K | ± 4.77K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48212.660   ± 1586.791  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1578.883    ± 293.855  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1279.287     ± 42.022  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1318.623    ± 186.090  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50779.838    ± 727.463  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65853.080   ± 1763.730  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56722.084    ± 213.111  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6426.609    ± 204.950  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6758.934     ± 31.144  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6451.177    ± 189.049  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        712.870     ± 26.686  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        580.425     ± 24.034  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6692.534    ± 848.148  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3028.222    ± 380.591  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4508.911     ± 18.129  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470313.141   ± 4767.491  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478627.611   ± 3648.051  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479760.165   ± 4655.000  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495832.518   ± 3595.148  ops/s
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
