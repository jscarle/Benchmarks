# Benchmark of different read-only list interfaces

```
BenchmarkDotNet v0.13.10, Windows 11 (10.0.22631.3155/23H2/2023Update/SunValley3)
13th Gen Intel Core i7-13700KF, 1 CPU, 24 logical and 16 physical cores
.NET SDK 8.0.200
  [Host]     : .NET 8.0.2 (8.0.224.6711), X64 RyuJIT AVX2
  DefaultJob : .NET 8.0.2 (8.0.224.6711), X64 RyuJIT AVX2
```

## Checking if the list contains any elements

| Method                         | Iterations | Mean     | Error    | StdDev   |
|------------------------------- |----------- |---------:|---------:|---------:|
| IEnumerable.Any()              | 100000     | 20.60 μs | 0.065 μs | 0.060 μs |
| IReadOnlyCollection.Count != 0 | 100000     | 18.90 μs | 0.057 μs | 0.054 μs |
| IReadOnlyList.Count != 0       | 100000     | 18.94 μs | 0.084 μs | 0.079 μs |

## Retrieving the first element in the list

| Method                      | Iterations | Mean     | Error   | StdDev  |
|---------------------------- |----------- |---------:|--------:|--------:|
| IEnumerable.First()         | 100000     | 626.2 μs | 5.26 μs | 4.92 μs |
| IReadOnlyCollection.First() | 100000     | 567.4 μs | 2.55 μs | 2.13 μs |
| IReadOnlyList[Indexer]      | 100000     | 132.6 μs | 0.69 μs | 0.64 μs |

## Combination of both

| Method              | Iterations | Mean     | Error   | StdDev  |
|-------------------- |----------- |---------:|--------:|--------:|
| IEnumerable         | 100000     | 574.1 μs | 3.86 μs | 3.61 μs |
| IReadOnlyCollection | 100000     | 580.6 μs | 3.32 μs | 3.11 μs |
| IReadOnlyList       | 100000     | 124.1 μs | 1.49 μs | 1.39 μs |
