# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-16T06:03:40Z
- **Commit:** [`9776bc9`](https://github.com/Draczech/client_java/commit/9776bc9ce102e5eff974b337fd6c44d97be0b8dd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.38K | ± 769.66 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.14K | ± 373.93 | ops/s | 1.2x slower |
| prometheusAdd | 48.30K | ± 688.91 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.01K | ± 190.83 | ops/s | 1.4x slower |
| simpleclientInc | 6.23K | ± 126.46 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.13K | ± 260.70 | ops/s | 9.9x slower |
| simpleclientAdd | 5.95K | ± 228.57 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.46K | ± 152.99 | ops/s | 41x slower |
| openTelemetryInc | 1.45K | ± 38.50 | ops/s | 42x slower |
| openTelemetryAdd | 1.35K | ± 68.32 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.47K | ± 117.62 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 47.25 | ops/s | 1.6x slower |
| prometheusNative | 2.94K | ± 268.25 | ops/s | 2.5x slower |
| openTelemetryClassic | 605.93 | ± 19.66 | ops/s | 12x slower |
| openTelemetryExponential | 524.30 | ± 36.25 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 536.85K | ± 3.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 528.93K | ± 1.86K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 517.76K | ± 1.25K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.29K | ± 6.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44012.557    ± 190.831  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1352.577     ± 68.319  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1446.572     ± 38.498  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1464.506    ± 152.987  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48300.021    ± 688.908  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60375.055    ± 769.662  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52137.944    ± 373.931  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5954.604    ± 228.565  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6225.245    ± 126.464  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6126.619    ± 260.704  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        605.926     ± 19.662  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        524.303     ± 36.247  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7466.037    ± 117.622  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2940.134    ± 268.245  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4550.099     ± 47.253  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509285.251   ± 6203.721  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     517762.202   ± 1253.292  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     528930.692   ± 1864.487  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     536849.057   ± 3786.637  ops/s
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
