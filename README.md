<!--
Copyright 2022-2023 cluetec GmbH and Contributors

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->

# Go Guide

Here you will find a collection of links, guides and examples to various topics related to Go programming.

## Getting Started

- [The Go Tour](https://go.dev/tour)
- [Effective Go](https://go.dev/doc/effective_go)
- [Standard Library](https://pkg.go.dev/std)
- [Go Playground](https://go.dev/play/)
- [Go Developer Roadmap.sh - Step by step guide to becoming a Go developer in 2023](https://roadmap.sh/golang)

## Installation

- [Official Doc](https://go.dev/doc/install)

## Best practices

- [Project Layout](https://github.com/golang-standards/project-layout/blob/master/README.md)
- [Design Patterns](https://github.com/tmrts/go-patterns)
- [Go Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)
- [100 Go Mistakes from Teiva Harsanyi](https://100go.co/)

### Slices

- <https://ueokande.github.io/go-slice-tricks/>
- <https://github.com/golang/go/wiki/SliceTricks>

### Structs

- [Validator](https://github.com/go-playground/validator) - Package for validating Structs

#### Initialization

A good (not the best as it depends on the situation) way to initialize a struct would be by implementing a "Constructor Method" with the required fields for the struct as arguments so that the consumer MUST pass them, and have everything else as optional parameters, which may be skipped.

Source: <https://asankov.dev/blog/2022/01/29/different-ways-to-initialize-go-structs/>

<details>
  <summary style="cursor: pointer">Expand</summary>

  ```go
  package people

  // Properties are package privat
  type Person struct {
    age    int
    name   string
  }

  type PersonOptions struct {
    Age *int
  }

  func NewPerson(name string, options *PersonOptions) *Person {
    p := &Person{name: name}
    if options == nil {
      return p
    }
    if options.Age != nil && options.Age != 0 {
      p.age = *options.Age
    }
    return p
  }
  ///////////////////////////////////////////////
  package main

  p := people.NewPerson("Anton", &people.PersonOptions{Age: 25})
  // or
  p := people.NewPerson("Anton", nil)
  ```

</details>

## JSON un-/marshaling

- [JSON to Go](https://mholt.github.io/json-to-go/)
- [Validator](https://github.com/go-playground/validator) - Package for validating Structs (and therefor also unmarshaled JSON)

## Concurrency

- <https://github.com/golang/go/wiki/LearnConcurrency>

## Tests

- <https://quii.gitbook.io/learn-go-with-tests/>

## Memory optimization

- <https://www.ribice.ba/golang-memory-savings/>
- <https://hmarr.com/blog/go-allocation-hunting/>

## Orchestration

### Dockerfile

A good example how to use a multi-stage container image for Go application is the [docker-compose-cli container image](https://github.com/docker/compose-cli/blob/main/Dockerfile).

Important regarding performance is to use a cache for all `RUN` commands which are using the Go binary. While `go build` go will use the cache to not rebuild the whole application which increases the performance a lot!

```Dockerfile
RUN --mount=type=cache,target=/go/pkg/mod \
    --mount=type=cache,target=/root/.cache/go-build \
    go mod download
```

## Vulnerability Management

```shell
go install golang.org/x/vuln/cmd/govulncheck@latest
govulncheck ./...
```

Source: <https://go.dev/blog/vuln>

## Licensing

- [ribice/glice](https://github.com/ribice/glice) - Shows a list with all dependencies and their licenses

## Examples

- [Go by example](https://gobyexample.com/)
- [DDD Project](https://github.com/ThreeDotsLabs/wild-workouts-go-ddd-example)

## Blogs

- [The Go Blog](https://go.dev/blog/)

## IDEs / Editor

### Visual-Studio Code (vscode)

#### Open monorepo without `go.work` file

**Problem:**

If you have a monorepo without using the go workspaces and you open this monorepo in vscode you will see errors in the code like this:

```plain
gopls was not able to find modules in your workspace.
When outside of GOPATH, gopls needs to know which modules you are working on.
You can fix this by opening your workspace to a folder inside a Go module, or
by using a go.work file to specify multiple modules.
See the documentation for more information on setting up your workspace:
https://github.com/golang/tools/blob/master/gopls/doc/workspace.md.go
```

**Solution:**

Those errors can mostly be resolved by adding the following experimental feature flag to your vscode settings:

```json
{
    "gopls": {
        "experimentalWorkspaceModule": true
    }
}
```

## Further links

- [Awesome-Go](https://awesome-go.com/)
- [Style Guide from Uber](https://github.com/uber-go/guide/blob/master/style.md)

## License

Copyright 2022-2024 [cluetec GmbH](https://www.cluetec.de/) and Contributors

The project is licensed under the [Apache License 2.0](./LICENSE).
