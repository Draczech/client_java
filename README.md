# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-26T06:34:20Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.90K | ± 818.64 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.30K | ± 747.42 | ops/s | 1.2x slower |
| prometheusAdd | 48.57K | ± 988.27 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 45.27K | ± 363.22 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.20K | ± 60.64 | ops/s | 9.8x slower |
| simpleclientInc | 6.11K | ± 169.50 | ops/s | 10.0x slower |
| simpleclientAdd | 5.95K | ± 193.81 | ops/s | 10x slower |
| openTelemetryInc | 1.49K | ± 187.04 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.42K | ± 14.60 | ops/s | 43x slower |
| openTelemetryAdd | 1.39K | ± 13.08 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.50K | ± 1.52K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 48.87 | ops/s | 1.2x slower |
| prometheusNative | 2.86K | ± 180.04 | ops/s | 1.9x slower |
| openTelemetryClassic | 624.14 | ± 23.51 | ops/s | 8.8x slower |
| openTelemetryExponential | 503.77 | ± 34.32 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 539.11K | ± 5.34K | ops/s | **fastest** |
| openMetricsWriteToNull | 523.97K | ± 2.78K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 519.96K | ± 8.84K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.92K | ± 3.77K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45269.228    ± 363.224  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1392.607     ± 13.084  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1494.942    ± 187.038  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1415.234     ± 14.600  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48567.114    ± 988.268  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60901.296    ± 818.643  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51298.136    ± 747.420  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5949.525    ± 193.810  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6107.447    ± 169.498  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6201.395     ± 60.639  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        624.136     ± 23.507  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        503.773     ± 34.322  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5497.566   ± 1517.679  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2860.358    ± 180.037  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4495.474     ± 48.874  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509924.623   ± 3768.837  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     523974.710   ± 2784.806  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     519956.592   ± 8843.657  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     539105.122   ± 5337.766  ops/s
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
