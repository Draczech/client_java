# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-27T07:00:25Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.99K | ± 426.14 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.11K | ± 224.30 | ops/s | 1.2x slower |
| prometheusAdd | 51.05K | ± 708.64 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.63K | ± 883.72 | ops/s | 1.4x slower |
| simpleclientInc | 6.55K | ± 50.17 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.43K | ± 131.12 | ops/s | 10x slower |
| simpleclientAdd | 6.08K | ± 38.74 | ops/s | 11x slower |
| openTelemetryInc | 1.83K | ± 236.18 | ops/s | 36x slower |
| openTelemetryAdd | 1.32K | ± 60.39 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.23K | ± 65.46 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.09K | ± 675.10 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 54.88 | ops/s | 1.2x slower |
| prometheusNative | 2.92K | ± 233.74 | ops/s | 1.7x slower |
| openTelemetryClassic | 696.18 | ± 41.31 | ops/s | 7.3x slower |
| openTelemetryExponential | 544.62 | ± 12.71 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.87K | ± 4.93K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.39K | ± 3.10K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.30K | ± 4.35K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.02K | ± 4.49K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48625.445    ± 883.722  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1321.932     ± 60.393  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1830.067    ± 236.179  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1231.738     ± 65.458  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51045.707    ± 708.637  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65994.560    ± 426.138  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57106.690    ± 224.297  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6079.372     ± 38.736  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6552.911     ± 50.171  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6426.218    ± 131.121  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        696.182     ± 41.308  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.622     ± 12.707  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5087.055    ± 675.101  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2917.598    ± 233.736  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4413.113     ± 54.877  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466018.911   ± 4488.088  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476296.424   ± 4346.766  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481390.230   ± 3101.041  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488872.927   ± 4931.754  ops/s
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
