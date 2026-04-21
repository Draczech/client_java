# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-21T05:55:18Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.34K | ± 787.89 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.04K | ± 158.89 | ops/s | 1.1x slower |
| prometheusAdd | 51.46K | ± 401.94 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.86K | ± 2.30K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 42.56 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.50K | ± 193.91 | ops/s | 10x slower |
| simpleclientAdd | 5.91K | ± 88.25 | ops/s | 11x slower |
| openTelemetryAdd | 1.42K | ± 268.77 | ops/s | 46x slower |
| openTelemetryInc | 1.39K | ± 149.92 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.20K | ± 32.65 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.44K | ± 76.76 | ops/s | **fastest** |
| prometheusClassic | 4.41K | ± 723.62 | ops/s | 1.0x slower |
| prometheusNative | 2.94K | ± 266.68 | ops/s | 1.5x slower |
| openTelemetryClassic | 749.71 | ± 10.30 | ops/s | 5.9x slower |
| openTelemetryExponential | 549.34 | ± 11.82 | ops/s | 8.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.99K | ± 1.39K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.14K | ± 3.53K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.61K | ± 4.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.05K | ± 5.36K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49858.029   ± 2302.382  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1424.605    ± 268.775  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1389.612    ± 149.923  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1199.943     ± 32.654  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51461.431    ± 401.942  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65342.671    ± 787.889  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57042.451    ± 158.894  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5913.929     ± 88.248  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6661.465     ± 42.562  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6500.613    ± 193.910  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        749.708     ± 10.295  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        549.336     ± 11.821  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4408.288    ± 723.616  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2942.510    ± 266.682  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4441.433     ± 76.759  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470049.436   ± 5358.908  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476613.975   ± 4098.878  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484136.640   ± 3527.613  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489986.415   ± 1390.430  ops/s
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
