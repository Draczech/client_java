# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-24T05:23:29Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.11K | ± 2.01K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.07K | ± 421.75 | ops/s | 1.1x slower |
| prometheusAdd | 51.40K | ± 380.97 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.18K | ± 182.71 | ops/s | 1.4x slower |
| simpleclientInc | 6.70K | ± 124.93 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.62K | ± 132.53 | ops/s | 9.7x slower |
| simpleclientAdd | 6.03K | ± 177.59 | ops/s | 11x slower |
| openTelemetryAdd | 1.61K | ± 238.79 | ops/s | 40x slower |
| openTelemetryInc | 1.38K | ± 183.53 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.19K | ± 57.00 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.06K | ± 300.86 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 60.50 | ops/s | 1.6x slower |
| prometheusNative | 2.99K | ± 228.64 | ops/s | 2.4x slower |
| openTelemetryClassic | 682.49 | ± 29.89 | ops/s | 10x slower |
| openTelemetryExponential | 560.56 | ± 25.11 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.33K | ± 5.15K | ops/s | **fastest** |
| openMetricsWriteToNull | 494.50K | ± 1.09K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 494.40K | ± 1.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 490.18K | ± 3.04K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47184.298    ± 182.712  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1607.520    ± 238.787  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1376.152    ± 183.525  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1189.798     ± 57.000  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51403.726    ± 380.969  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64112.410   ± 2006.479  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57071.518    ± 421.745  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6032.392    ± 177.588  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6700.070    ± 124.934  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6619.063    ± 132.525  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.494     ± 29.891  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.563     ± 25.115  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7055.593    ± 300.861  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2989.634    ± 228.636  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4542.107     ± 60.496  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     490177.477   ± 3042.878  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     494501.243   ± 1092.082  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494402.302   ± 1364.851  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502326.511   ± 5153.190  ops/s
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
