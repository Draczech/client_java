# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-11T06:06:58Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.49K | ± 1.59K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.34K | ± 976.56 | ops/s | 1.2x slower |
| prometheusAdd | 51.14K | ± 255.23 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.17K | ± 1.58K | ops/s | 1.4x slower |
| simpleclientInc | 6.42K | ± 74.21 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.37K | ± 178.92 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 91.57 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.43K | ± 167.05 | ops/s | 46x slower |
| openTelemetryInc | 1.28K | ± 38.08 | ops/s | 51x slower |
| openTelemetryAdd | 1.27K | ± 53.06 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.62K | ± 426.24 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 53.90 | ops/s | 1.5x slower |
| prometheusNative | 2.83K | ± 297.29 | ops/s | 2.3x slower |
| openTelemetryClassic | 667.83 | ± 41.13 | ops/s | 9.9x slower |
| openTelemetryExponential | 551.11 | ± 19.00 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 479.28K | ± 3.93K | ops/s | **fastest** |
| prometheusWriteToByteArray | 474.95K | ± 4.91K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.37K | ± 3.82K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.22K | ± 3.52K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48170.033   ± 1584.102  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1273.830     ± 53.061  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1281.565     ± 38.084  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1431.187    ± 167.051  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51137.920    ± 255.231  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65485.704   ± 1588.206  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56340.826    ± 976.556  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6177.464     ± 91.568  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6420.087     ± 74.214  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6367.342    ± 178.917  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        667.827     ± 41.131  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.109     ± 19.001  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6618.211    ± 426.238  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2827.682    ± 297.288  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4439.645     ± 53.901  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467221.184   ± 3523.394  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473369.691   ± 3815.970  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     474954.129   ± 4909.011  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     479277.714   ± 3931.261  ops/s
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
