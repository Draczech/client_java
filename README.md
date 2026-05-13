# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-13T06:55:29Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.40K | ± 1.20K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.92K | ± 2.36K | ops/s | 1.2x slower |
| prometheusAdd | 48.92K | ± 3.11K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.94K | ± 886.90 | ops/s | 1.4x slower |
| simpleclientInc | 6.60K | ± 172.46 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.40K | ± 137.58 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 242.07 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 170.83 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.29K | ± 155.50 | ops/s | 50x slower |
| openTelemetryAdd | 1.23K | ± 53.27 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.02K | ± 2.20K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 39.09 | ops/s | 1.4x slower |
| prometheusNative | 3.02K | ± 315.83 | ops/s | 2.0x slower |
| openTelemetryClassic | 671.28 | ± 25.13 | ops/s | 9.0x slower |
| openTelemetryExponential | 577.12 | ± 12.82 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.99K | ± 3.16K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.80K | ± 2.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.88K | ± 11.11K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.09K | ± 4.91K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46942.712    ± 886.904  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1230.670     ± 53.272  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1357.689    ± 170.834  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1286.990    ± 155.495  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48922.091   ± 3106.392  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64404.431   ± 1201.928  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54923.931   ± 2363.503  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6334.639    ± 242.073  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6595.520    ± 172.460  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6402.647    ± 137.584  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        671.280     ± 25.127  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        577.124     ± 12.818  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6017.664   ± 2201.102  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3017.372    ± 315.827  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4380.802     ± 39.089  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475086.657   ± 4908.972  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476876.335  ± 11112.098  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487795.427   ± 2230.928  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490989.813   ± 3164.844  ops/s
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
