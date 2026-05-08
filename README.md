# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-08T06:02:56Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.75K | ± 703.14 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.24K | ± 173.47 | ops/s | 1.2x slower |
| prometheusAdd | 51.22K | ± 336.73 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.02K | ± 1.70K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.61K | ± 21.91 | ops/s | 10x slower |
| simpleclientInc | 6.53K | ± 188.90 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 173.53 | ops/s | 11x slower |
| openTelemetryAdd | 1.40K | ± 312.31 | ops/s | 48x slower |
| openTelemetryInc | 1.39K | ± 172.95 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.29K | ± 258.06 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.29K | ± 822.19 | ops/s | **fastest** |
| simpleclient | 4.49K | ± 33.57 | ops/s | 1.4x slower |
| prometheusNative | 2.99K | ± 290.23 | ops/s | 2.1x slower |
| openTelemetryClassic | 651.59 | ± 19.50 | ops/s | 9.6x slower |
| openTelemetryExponential | 565.52 | ± 6.06 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.74K | ± 1.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.82K | ± 2.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.22K | ± 2.68K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 484.45K | ± 2.48K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49018.591   ± 1696.567  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1404.565    ± 312.311  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1392.787    ± 172.953  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1286.647    ± 258.058  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51224.309    ± 336.729  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66745.303    ± 703.144  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57244.275    ± 173.468  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6338.136    ± 173.532  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6533.153    ± 188.905  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6606.159     ± 21.910  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        651.593     ± 19.501  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.516      ± 6.063  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6285.897    ± 822.188  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2991.623    ± 290.228  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4494.577     ± 33.567  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     484452.904   ± 2476.800  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487221.339   ± 2681.727  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490817.763   ± 2287.924  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493740.491   ± 1939.789  ops/s
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
