# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-12T07:53:23Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.00K | ± 1.83K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.05K | ± 432.59 | ops/s | 1.1x slower |
| prometheusAdd | 51.42K | ± 249.56 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.21K | ± 1.57K | ops/s | 1.3x slower |
| simpleclientInc | 6.71K | ± 9.87 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.34K | ± 234.08 | ops/s | 10x slower |
| simpleclientAdd | 5.93K | ± 123.94 | ops/s | 11x slower |
| openTelemetryInc | 1.39K | ± 101.85 | ops/s | 47x slower |
| openTelemetryAdd | 1.39K | ± 231.82 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.33K | ± 214.96 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.44K | ± 1.07K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 58.89 | ops/s | 1.5x slower |
| prometheusNative | 2.92K | ± 250.21 | ops/s | 2.2x slower |
| openTelemetryClassic | 749.50 | ± 64.09 | ops/s | 8.6x slower |
| openTelemetryExponential | 560.04 | ± 25.61 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.51K | ± 4.92K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.95K | ± 5.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.89K | ± 2.38K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.42K | ± 5.09K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49212.073   ± 1574.870  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1390.258    ± 231.821  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1391.423    ± 101.849  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1334.478    ± 214.961  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51417.364    ± 249.557  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64996.821   ± 1829.905  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57049.007    ± 432.586  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5928.732    ± 123.937  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6706.420      ± 9.865  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6335.336    ± 234.082  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        749.499     ± 64.086  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.035     ± 25.613  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6436.909   ± 1065.889  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2916.651    ± 250.211  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4415.421     ± 58.893  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464420.135   ± 5091.162  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478887.577   ± 2379.906  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485945.528   ± 5820.352  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486509.290   ± 4922.765  ops/s
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
