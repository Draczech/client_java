# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-08T06:11:58Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.25K | ± 742.23 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.86K | ± 790.54 | ops/s | 1.2x slower |
| prometheusAdd | 48.70K | ± 696.06 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.64K | ± 1.63K | ops/s | 1.4x slower |
| simpleclientInc | 6.25K | ± 43.23 | ops/s | 9.6x slower |
| simpleclientAdd | 6.08K | ± 176.28 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.85K | ± 77.47 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.49K | ± 95.01 | ops/s | 41x slower |
| openTelemetryInc | 1.47K | ± 94.44 | ops/s | 41x slower |
| openTelemetryAdd | 1.37K | ± 79.40 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.41K | ± 1.20K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 62.98 | ops/s | 1.2x slower |
| prometheusNative | 2.92K | ± 286.58 | ops/s | 1.9x slower |
| openTelemetryClassic | 625.47 | ± 38.70 | ops/s | 8.7x slower |
| openTelemetryExponential | 525.81 | ± 4.65 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.81K | ± 2.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 525.96K | ± 4.77K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 522.98K | ± 5.33K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 508.13K | ± 831.17 | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43643.703   ± 1633.334  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1370.413     ± 79.399  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1469.243     ± 94.442  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1486.391     ± 95.012  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48703.398    ± 696.057  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60254.928    ± 742.235  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51861.137    ± 790.543  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6077.349    ± 176.277  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6248.533     ± 43.225  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5849.854     ± 77.473  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        625.468     ± 38.703  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        525.810      ± 4.649  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5410.933   ± 1198.225  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2917.653    ± 286.580  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4513.260     ± 62.980  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508126.383    ± 831.172  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     522982.406   ± 5326.536  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     525960.972   ± 4768.538  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532814.805   ± 2858.734  ops/s
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
