## httpstress-go [![Build Status](https://travis-ci.org/chillum/httpstress-go.svg?branch=master)](https://travis-ci.org/chillum/httpstress-go)

httpstress-go is a CLI utility for stress testing of HTTP servers with many concurrent connections.

Returns 0 if no errors, 1 if some failed (see stdout), 2 on kill, 3 in case of invalid options
and 4 if it encounters a setrlimit(2)/getrlimit(2) error.

Prints error count for each URL to stdout (does not count successful attempts).
Errors and debugging information go to stderr.

### Installing from binaries
Extract the appropriate archive and launch `httpstress-go` with desired options

* Windows
  * [64-bit Windows](https://github.com/chillum/httpstress-go/releases/download/v2.2/win64.zip) (recommended)
  * [32-bit Windows](https://github.com/chillum/httpstress-go/releases/download/v2.2/win32.zip)
* [Mac OS X](https://github.com/chillum/httpstress-go/releases/download/v2.2/mac.zip) (10.7 or greater)
* Linux
  * [x86-64 Linux](https://github.com/chillum/httpstress-go/releases/download/v2.2/linux_amd64.zip) (recommended)
  * [i386 Linux](https://github.com/chillum/httpstress-go/releases/download/v2.2/linux_386.zip)

### Installing from source
* Supported platforms: Unix and Windows
* Install [Git](http://git-scm.com/download)
* Install [Go runtime](http://golang.org/doc/install).
  Go 1.3 or higher on amd64 is recommended because of performance issues
* Set [`GOPATH`](http://golang.org/doc/code.html#GOPATH)
* `go get github.com/chillum/httpstress-go`
* `httpstress-go` is
  [a static-linked binary](http://golang.org/doc/faq#Why_is_my_trivial_program_such_a_large_binary),
  it's possible to deploy it just by copying `$GOPATH/bin/httpstress-go`
  (`%GOPATH%\bin\httpstress-go.exe` on Windows),
  compiled on matching system and architecture
* Ready to use: launch `httpstress-go` with desired options

### Environment
`GOMAXPROCS` – Go threads number (defaults to CPU count + 1)

### Usage
`httpstress-go <URL list> [options]`

### Options
* `URL list` – URLs to fetch (required)
* `-c NUM` – concurrent connections number (defaults to 1)
* `-n NUM` – total connections number (optional)
* `-v` – print version to stdout and exit

### Example usage
`httpstress-go http://localhost https://google.com -c 1000`

### Notes
* This ulility takes care of `ulimit -n` on Unix systems: sets it to
  the value of `-c` option plus 6, if the current limit is smaller.
* Error output is YAML-formatted. Example:
```yaml
errors:
  - location: http://localhost
    count:    334
  - location: http://127.0.0.1
    count:    333
```
