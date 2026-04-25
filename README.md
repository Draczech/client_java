# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-25T05:42:35Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.38K | ± 692.56 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.08K | ± 563.79 | ops/s | 1.2x slower |
| prometheusAdd | 47.89K | ± 123.17 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.74K | ± 559.58 | ops/s | 1.3x slower |
| simpleclientInc | 6.36K | ± 17.33 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.19K | ± 174.46 | ops/s | 9.7x slower |
| simpleclientAdd | 5.94K | ± 151.61 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.42K | ± 79.62 | ops/s | 42x slower |
| openTelemetryAdd | 1.29K | ± 6.12 | ops/s | 47x slower |
| openTelemetryInc | 1.27K | ± 78.07 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.98K | ± 2.03K | ops/s | **fastest** |
| simpleclient | 4.33K | ± 54.82 | ops/s | 1.6x slower |
| prometheusNative | 3.16K | ± 46.59 | ops/s | 2.2x slower |
| openTelemetryClassic | 592.65 | ± 5.05 | ops/s | 12x slower |
| openTelemetryExponential | 510.19 | ± 14.45 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 549.86K | ± 10.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 535.03K | ± 7.25K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.97K | ± 1.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 517.25K | ± 1.51K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44736.528    ± 559.582  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1286.960      ± 6.123  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1269.856     ± 78.070  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1424.320     ± 79.619  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47892.225    ± 123.172  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60376.361    ± 692.563  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52080.027    ± 563.785  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5942.450    ± 151.613  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6363.910     ± 17.325  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6193.611    ± 174.456  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        592.646      ± 5.052  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        510.190     ± 14.450  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6978.549   ± 2031.138  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3160.184     ± 46.589  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4325.675     ± 54.816  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     517248.953   ± 1510.002  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534968.832   ± 1939.248  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     535025.027   ± 7245.798  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     549855.649  ± 10214.052  ops/s
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
