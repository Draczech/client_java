# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-15T08:08:03Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 31.25K | ± 87.56 | ops/s | **fastest** |
| prometheusInc | 30.09K | ± 220.56 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 30.08K | ± 256.15 | ops/s | 1.0x slower |
| prometheusAdd | 29.17K | ± 259.33 | ops/s | 1.1x slower |
| simpleclientAdd | 7.46K | ± 60.65 | ops/s | 4.2x slower |
| simpleclientInc | 7.44K | ± 143.10 | ops/s | 4.2x slower |
| simpleclientNoLabelsInc | 7.38K | ± 64.06 | ops/s | 4.2x slower |
| openTelemetryIncNoLabels | 1.20K | ± 79.45 | ops/s | 26x slower |
| openTelemetryAdd | 1.15K | ± 122.39 | ops/s | 27x slower |
| openTelemetryInc | 1.13K | ± 89.78 | ops/s | 28x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.70K | ± 84.56 | ops/s | **fastest** |
| prometheusClassic | 3.01K | ± 800.96 | ops/s | 1.6x slower |
| prometheusNative | 2.42K | ± 106.29 | ops/s | 1.9x slower |
| openTelemetryClassic | 400.32 | ± 22.81 | ops/s | 12x slower |
| openTelemetryExponential | 329.50 | ± 7.69 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 302.86K | ± 1.61K | ops/s | **fastest** |
| prometheusWriteToNull | 298.62K | ± 3.75K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 288.73K | ± 1.98K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 279.44K | ± 1.94K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      31250.864     ± 87.557  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1146.852    ± 122.387  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1125.242     ± 89.783  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1203.395     ± 79.454  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      29167.834    ± 259.328  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30089.915    ± 220.556  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30076.132    ± 256.150  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7462.595     ± 60.648  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7442.532    ± 143.096  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7375.171     ± 64.062  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        400.321     ± 22.806  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        329.503      ± 7.692  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3014.509    ± 800.957  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2422.370    ± 106.288  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4696.061     ± 84.555  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     279444.379   ± 1944.236  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     288725.767   ± 1977.698  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     302856.919   ± 1609.857  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     298618.046   ± 3746.271  ops/s
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
