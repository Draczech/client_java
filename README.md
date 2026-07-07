# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-07T07:13:10Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.66K | ± 1.79K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.65K | ± 2.32K | ops/s | 1.2x slower |
| prometheusAdd | 51.57K | ± 109.66 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.09K | ± 1.56K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.61K | ± 8.46 | ops/s | 9.8x slower |
| simpleclientInc | 6.47K | ± 183.63 | ops/s | 10.0x slower |
| simpleclientAdd | 6.31K | ± 237.45 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.33K | ± 218.91 | ops/s | 49x slower |
| openTelemetryAdd | 1.31K | ± 120.72 | ops/s | 49x slower |
| openTelemetryInc | 1.25K | ± 70.39 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.00K | ± 2.77K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 43.16 | ops/s | 1.6x slower |
| prometheusNative | 2.74K | ± 355.54 | ops/s | 2.6x slower |
| openTelemetryClassic | 691.36 | ± 40.00 | ops/s | 10x slower |
| openTelemetryExponential | 595.28 | ± 6.52 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 477.34K | ± 1.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 472.20K | ± 3.74K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 460.38K | ± 6.73K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 459.40K | ± 12.12K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49093.894   ± 1559.729  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1306.748    ± 120.718  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1251.227     ± 70.391  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1328.364    ± 218.911  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51569.672    ± 109.656  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64656.133   ± 1788.123  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55645.205   ± 2316.169  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6312.839    ± 237.450  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6473.134    ± 183.626  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6608.927      ± 8.464  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.361     ± 40.004  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        595.281      ± 6.520  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6996.093   ± 2765.984  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2736.192    ± 355.535  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4426.248     ± 43.165  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459398.746  ± 12123.567  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     460380.246   ± 6727.349  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     472204.419   ± 3739.636  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     477342.089   ± 1447.266  ops/s
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
