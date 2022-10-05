# Go Guide

## Getting Started

- [The Go Tour](https://go.dev/tour)
- [Effective Go](https://go.dev/doc/effective_go)
- [Standard Library](https://pkg.go.dev/std)
- [Go Playground](https://go.dev/play/)

## Installation

- [Official Doc](https://go.dev/doc/install)

## Best practices

- [Project Layout](https://github.com/golang-standards/project-layout/blob/master/README.md)
- [Design Patterns](https://github.com/tmrts/go-patterns)

### Slices

- <https://ueokande.github.io/go-slice-tricks/>
- <https://github.com/golang/go/wiki/SliceTricks>

## Concurrency

- https://github.com/golang/go/wiki/LearnConcurrency

## Tests

- https://quii.gitbook.io/learn-go-with-tests/

## Memory optimization

- https://www.ribice.ba/golang-memory-savings/

## Orchestration

### Dockerfile

A good example how to use a multi-stage container image for Go application is the [docker-compose-cli container image](https://github.com/docker/compose-cli/blob/main/Dockerfile).

Important regarding performance is to use a cache for all `RUN` commands which are using the Go binary. While `go build` go will use the cache to not rebuild the whole application which increases the performance a lot!

```Dockerfile
RUN --mount=type=cache,target=/go/pkg/mod \
    --mount=type=cache,target=/root/.cache/go-build \
    go mod download
```

## Examples

- [Go by example](https://gobyexample.com/)
- [DDD Project](https://github.com/ThreeDotsLabs/wild-workouts-go-ddd-example)

## Blogs

- [The Go Blog](https://go.dev/blog/)

## Further links

- [Awesome-Go](https://awesome-go.com/)
- [Style Guide from Uber](https://github.com/uber-go/guide/blob/master/style.md)

