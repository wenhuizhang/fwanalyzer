# Building FwAnalyzer

## Go Env
```
wenhui@wenhui:~/Downloads/xfstests-dev$ go env
GO111MODULE=""
GOARCH="amd64"
GOBIN=""
GOCACHE="/home/wenhui/.cache/go-build"
GOENV="/home/wenhui/.config/go/env"
GOEXE=""
GOFLAGS=""
GOHOSTARCH="amd64"
GOHOSTOS="linux"
GONOPROXY=""
GONOSUMDB=""
GOOS="linux"
GOPATH="/home/wenhui/go"
GOPRIVATE=""
GOPROXY="https://proxy.golang.org,direct"
GOROOT="/usr/lib/go-1.13"
GOSUMDB="sum.golang.org"
GOTMPDIR=""
GOTOOLDIR="/usr/lib/go-1.13/pkg/tool/linux_amd64"
GCCGO="gccgo"
AR="ar"
CC="gcc"
CXX="g++"
CGO_ENABLED="1"
GOMOD=""
CGO_CFLAGS="-g -O2"
CGO_CPPFLAGS=""
CGO_CXXFLAGS="-g -O2"
CGO_FFLAGS="-g -O2"
CGO_LDFLAGS="-g -O2"
PKG_CONFIG="pkg-config"
GOGCCFLAGS="-fPIC -m64 -pthread -fmessage-length=0 -fdebug-prefix-map=/tmp/go-build576806211=/tmp/go-build -gno-record-gcc-switches"

```


## Requirements

- golang + dep + golang-lint
- Python
- filesystem tools such as e2tools, mtools

The full list of dependencies is tracked in the [Dockerfile](Dockerfile).


```sh
 sudo add-apt-repository ppa:longsleep/golang-backports
 sudo apt-get update 
 sudo apt-get install golang-go python 
 go env
 curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
 sudo apt update && apt -y install e2tools mtools file squashfs-tools unzip python-setuptools python-lzo
 sudo apt update && sudo apt -y install e2tools mtools file squashfs-tools unzip python-setuptools python-lzo
 wget https://github.com/crmulliner/ubi_reader/archive/master.zip -O ubireader.zip && unzip ubireader.zip && cd ubi_reader-master && python setup.py install
```


## Clone Repository

```sh
cd go/src/github.com/cruise-automation/
git clone git@github.com:cruise-automation/fwanalyzer.git
```

## Building

Before building you need to download some third party go libraries, run `make deps` before the first build.

```sh
cd go/src/github.com/cruise-automation/fwanalyzer
make deps
make
```

The `fwanalyzer` binary will be in `build/`.

# Testing

We have two types of tests: unit tests and integration tests, both tests will be triggered by running `make test`.
Tests rely on e2tools, mtools, squashfs-tools, and ubi_reader, as well as Python.

```sh
cd go/src/github.com/cruise-automation/fwanalyzer
make test
```
