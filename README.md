# Process List Library for Go [![GoDoc](https://godoc.org/github.com/mitchellh/go-ps?status.png)](https://godoc.org/github.com/mitchellh/go-ps)

go-ps is a library for Go that implements OS-specific APIs to list and
manipulate processes in a platform-safe way. The library can find and
list processes on Linux, Mac OS X, Solaris, and Windows.

If you're new to Go, this library has a good amount of advanced Go educational
value as well. It uses some advanced features of Go: build tags, accessing
DLL methods for Windows, cgo for Darwin, etc.

How it works:

  * **Darwin** uses the `sysctl` syscall to retrieve the process table.
  * **Unix** uses the procfs at `/proc` to inspect the process tree.
  * **Windows** uses the Windows API, and methods such as
    `CreateToolhelp32Snapshot` to get a point-in-time snapshot of
    the process table.

## Installation

Install using standard `go get`:

```
$ go get github.com/mitchellh/go-ps
...
```

import (
      ps "github.com/mitchellh/go-ps"
      ... // other imports here...
)

```
func whatever(){
    processList, err := ps.Processes()
    if err != nil {
        log.Println("ps.Processes() Failed, are you using windows?")
        return
    }

    // map ages
    for x := range processList {
        var process ps.Process
        process = processList[x]
        log.Printf("%d\t%s\n",process.Pid(),process.Executable())

        // do os.* stuff on the pid
    }
}
```
