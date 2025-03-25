---
title: "Testing and Benchmarks"
weight: 3
---

### [&#128279;](#testing-and-benchmarks) Testing and Benchmarks

The Go module contains unit tests, integration tests, and benchmarks.

#### UI Integration Tests

Playwright is used to do integration testing as well as record basic demo videos with `ffmpeg`.

```
make go_test_main
```

#### Unit Tests and Benchmarks

A unit testing framework incorporating `gomocks` interface mocks allows for API testing. Benchmarks may also be added and will be run as well.

```
make go_test_pkg
```

