# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-14T05:52:13Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.01K | ± 656.58 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.74K | ± 453.44 | ops/s | 1.1x slower |
| prometheusAdd | 51.45K | ± 135.47 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.54K | ± 2.52K | ops/s | 1.3x slower |
| simpleclientInc | 6.48K | ± 187.93 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.44K | ± 180.08 | ops/s | 9.9x slower |
| simpleclientAdd | 6.31K | ± 288.14 | ops/s | 10x slower |
| openTelemetryInc | 1.35K | ± 185.89 | ops/s | 47x slower |
| openTelemetryAdd | 1.33K | ± 93.19 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.33K | ± 182.39 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.59K | ± 2.19K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 40.52 | ops/s | 1.5x slower |
| prometheusNative | 3.04K | ± 265.39 | ops/s | 2.2x slower |
| openTelemetryClassic | 723.01 | ± 30.95 | ops/s | 9.1x slower |
| openTelemetryExponential | 540.04 | ± 15.05 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.65K | ± 2.77K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.93K | ± 2.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.91K | ± 5.26K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.56K | ± 1.64K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49538.376   ± 2517.464  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1333.093     ± 93.190  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1348.767    ± 185.894  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1327.060    ± 182.385  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51446.173    ± 135.472  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64008.119    ± 656.583  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56740.484    ± 453.444  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6306.044    ± 288.143  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6480.638    ± 187.928  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6441.439    ± 180.085  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        723.012     ± 30.954  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        540.042     ± 15.054  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6587.323   ± 2194.949  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3043.238    ± 265.392  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4463.943     ± 40.520  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477559.551   ± 1636.695  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479909.785   ± 5258.637  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486930.698   ± 2939.004  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493654.777   ± 2774.737  ops/s
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
