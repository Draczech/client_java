# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-10T07:06:24Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.99K | ± 1.24K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.37K | ± 2.14K | ops/s | 1.2x slower |
| prometheusAdd | 51.66K | ± 83.39 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.92K | ± 1.70K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 56.05 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.40K | ± 172.62 | ops/s | 10x slower |
| simpleclientAdd | 6.08K | ± 323.32 | ops/s | 11x slower |
| openTelemetryInc | 1.41K | ± 226.48 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.22K | ± 65.77 | ops/s | 54x slower |
| openTelemetryAdd | 1.20K | ± 53.64 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.89K | ± 1.59K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 16.71 | ops/s | 1.3x slower |
| prometheusNative | 2.79K | ± 203.24 | ops/s | 2.1x slower |
| openTelemetryClassic | 692.28 | ± 58.83 | ops/s | 8.5x slower |
| openTelemetryExponential | 548.63 | ± 18.41 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.70K | ± 2.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.38K | ± 3.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.19K | ± 5.15K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.90K | ± 8.72K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48919.028   ± 1696.857  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1200.706     ± 53.643  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1407.594    ± 226.480  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1223.111     ± 65.770  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51658.788     ± 83.389  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65994.382   ± 1235.554  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55371.489   ± 2139.632  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6079.474    ± 323.320  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6658.848     ± 56.055  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6396.703    ± 172.620  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        692.280     ± 58.834  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.628     ± 18.408  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5889.025   ± 1587.778  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2794.956    ± 203.245  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4457.436     ± 16.712  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467899.767   ± 8719.010  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475192.981   ± 5149.287  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481381.469   ± 3671.887  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485698.280   ± 2153.957  ops/s
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
