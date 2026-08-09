# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-09T04:38:38Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 72.15K | ± 4.07K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.03K | ± 1.14K | ops/s | 1.1x slower |
| prometheusAdd | 62.28K | ± 297.94 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 55.77K | ± 1.60K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 8.13K | ± 11.10 | ops/s | 8.9x slower |
| simpleclientInc | 8.03K | ± 166.92 | ops/s | 9.0x slower |
| simpleclientAdd | 7.95K | ± 71.37 | ops/s | 9.1x slower |
| openTelemetryInc | 1.87K | ± 176.44 | ops/s | 39x slower |
| openTelemetryAdd | 1.79K | ± 191.09 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.77K | ± 68.10 | ops/s | 41x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 8.01K | ± 2.37K | ops/s | **fastest** |
| simpleclient | 5.86K | ± 87.18 | ops/s | 1.4x slower |
| prometheusNative | 4.07K | ± 19.68 | ops/s | 2.0x slower |
| openTelemetryClassic | 807.20 | ± 16.77 | ops/s | 9.9x slower |
| openTelemetryExponential | 678.54 | ± 25.45 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 675.32K | ± 8.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 662.98K | ± 5.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 653.28K | ± 5.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 637.75K | ± 4.69K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55768.264   ± 1601.781  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1788.012    ± 191.091  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1872.829    ± 176.442  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1770.058     ± 68.100  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62280.237    ± 297.940  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      72148.783   ± 4072.828  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66027.928   ± 1139.862  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7946.257     ± 71.371  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8025.555    ± 166.917  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8134.871     ± 11.101  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        807.205     ± 16.770  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        678.540     ± 25.445  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8012.103   ± 2370.553  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4072.350     ± 19.677  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5859.597     ± 87.183  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     637753.907   ± 4692.718  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     653278.072   ± 5474.405  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     662980.434   ± 5674.964  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     675320.846   ± 8938.357  ops/s
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
