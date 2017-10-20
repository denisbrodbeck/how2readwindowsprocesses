# How to read windows processes from golang (without going crazy)

Need a list of all windows processes? Or need the PID of a specific process, but you've only got a name?

## How it works

This repository shows the main parts needed to get a process list:

* Create a snapshot of the current windows process list using `CreateToolhelp32Snapshot`.
* Fetch the first process in the snapshot list with `Process32First`.
* Keep iterating with `Process32Next`, until you get the `ERROR_NO_MORE_FILES` error, which is your cue to finish.

## Installation

```bash
go get github.com/denisbrodbeck/how2readwindowsprocesses
```

On Windows you can build it directly with `go build main.go`.

On Linux/OSX you need to target the correct environment:

```bash
GOOS=windows GOARCH=amd64 go build -o bin/processes.exe  main.go
# or
GOOS=windows GOARCH=386 go build -o bin/processes.exe  main.go
```

If you are missing dependencies, you can install them with [dep](https://github.com/golang/dep):

```bash
cd "$GOPATH/src/github.com/denisbrodbeck/how2readwindowsprocesses"
dep init
```
