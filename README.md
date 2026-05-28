# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-28T07:15:06Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.36K | ± 809.60 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.53K | ± 407.06 | ops/s | 1.2x slower |
| prometheusAdd | 48.96K | ± 750.48 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 41.16K | ± 4.82K | ops/s | 1.5x slower |
| simpleclientInc | 6.17K | ± 118.65 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.14K | ± 199.37 | ops/s | 9.8x slower |
| simpleclientAdd | 5.95K | ± 137.33 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.51K | ± 133.18 | ops/s | 40x slower |
| openTelemetryAdd | 1.45K | ± 74.04 | ops/s | 41x slower |
| openTelemetryInc | 1.42K | ± 158.91 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.08K | ± 1.31K | ops/s | **fastest** |
| simpleclient | 4.22K | ± 197.37 | ops/s | 1.4x slower |
| prometheusNative | 3.16K | ± 22.79 | ops/s | 1.9x slower |
| openTelemetryClassic | 636.92 | ± 17.35 | ops/s | 9.6x slower |
| openTelemetryExponential | 527.98 | ± 32.52 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 531.66K | ± 3.61K | ops/s | **fastest** |
| prometheusWriteToByteArray | 523.16K | ± 4.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 512.50K | ± 3.46K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 500.02K | ± 5.40K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      41159.950   ± 4817.057  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1454.826     ± 74.039  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1415.988    ± 158.912  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1511.386    ± 133.176  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48957.227    ± 750.485  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60363.059    ± 809.595  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51527.571    ± 407.058  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5948.209    ± 137.332  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6165.499    ± 118.653  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6142.019    ± 199.371  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        636.917     ± 17.346  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        527.978     ± 32.518  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6084.920   ± 1309.316  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3162.404     ± 22.790  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4218.606    ± 197.368  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     500015.439   ± 5400.886  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     512497.132   ± 3460.635  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     523164.804   ± 4291.909  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     531664.473   ± 3606.246  ops/s
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
