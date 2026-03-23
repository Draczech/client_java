# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-23T05:31:55Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.82K | ± 851.73 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.10K | ± 105.99 | ops/s | 1.2x slower |
| prometheusAdd | 51.44K | ± 531.60 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.89K | ± 605.04 | ops/s | 1.3x slower |
| simpleclientInc | 6.71K | ± 180.03 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.61K | ± 134.42 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 178.51 | ops/s | 11x slower |
| openTelemetryAdd | 1.45K | ± 249.52 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.37K | ± 196.24 | ops/s | 49x slower |
| openTelemetryInc | 1.34K | ± 169.57 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 1.49K | ops/s | **fastest** |
| simpleclient | 4.59K | ± 33.95 | ops/s | 1.1x slower |
| prometheusNative | 2.96K | ± 237.23 | ops/s | 1.8x slower |
| openTelemetryClassic | 686.15 | ± 20.10 | ops/s | 7.6x slower |
| openTelemetryExponential | 559.01 | ± 13.77 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 483.81K | ± 8.53K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.10K | ± 7.74K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.20K | ± 10.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.13K | ± 7.95K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49893.665    ± 605.040  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1448.651    ± 249.520  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1342.247    ± 169.565  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1365.577    ± 196.244  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51441.086    ± 531.599  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66823.841    ± 851.735  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57103.652    ± 105.989  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6305.224    ± 178.507  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6708.905    ± 180.033  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6609.726    ± 134.415  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.148     ± 20.102  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.015     ± 13.772  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5244.829   ± 1494.380  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2955.181    ± 237.231  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4589.225     ± 33.954  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466133.353   ± 7951.797  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471197.949  ± 10987.872  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481103.496   ± 7738.528  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     483811.852   ± 8533.668  ops/s
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
