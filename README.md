# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-07T05:39:43Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.28K | ± 738.28 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.29K | ± 1.00K | ops/s | 1.2x slower |
| prometheusAdd | 51.36K | ± 150.46 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.45K | ± 1.64K | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 161.75 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.47K | ± 236.82 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 278.04 | ops/s | 11x slower |
| openTelemetryInc | 1.39K | ± 174.17 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.34K | ± 202.59 | ops/s | 49x slower |
| openTelemetryAdd | 1.26K | ± 32.15 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 1.36K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 11.77 | ops/s | 1.2x slower |
| prometheusNative | 2.62K | ± 115.43 | ops/s | 2.0x slower |
| openTelemetryClassic | 702.61 | ± 18.08 | ops/s | 7.6x slower |
| openTelemetryExponential | 574.90 | ± 12.75 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.07K | ± 4.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.02K | ± 1.57K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.34K | ± 1.98K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.24K | ± 6.62K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49451.647   ± 1635.471  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1263.022     ± 32.152  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1385.426    ± 174.166  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1339.088    ± 202.590  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51364.450    ± 150.456  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66280.038    ± 738.278  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56287.756   ± 1000.890  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6302.554    ± 278.039  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6588.998    ± 161.753  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6473.038    ± 236.815  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        702.610     ± 18.077  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        574.895     ± 12.749  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5356.875   ± 1360.283  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2622.196    ± 115.430  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4397.185     ± 11.771  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475237.681   ± 6620.940  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481339.022   ± 1982.752  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486018.760   ± 1574.644  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490065.858   ± 4889.127  ops/s
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
