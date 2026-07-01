# CAPA (Common Analysis Platform for Artifacts)

## What is CAPA?

**CAPA** is a **static malware analysis tool** developed by **FireEye Mandiant**.

It analyzes executable files and automatically identifies **what the program is capable of doing** without running it.

Instead of telling you **how** malware works internally, CAPA tells you **what capabilities** it has.


# Why Use CAPA?

Manually reverse engineering malware takes a lot of time.

CAPA automates this process by using thousands of predefined rules.

It quickly answers questions like:

* Can this malware access files?
* Can it communicate over the network?
* Can it inject code into another process?
* Can it modify the registry?
* Can it create persistence?


# Static Analysis vs Dynamic Analysis

| Static Analysis               | Dynamic Analysis                  |
| ----------------------------- | --------------------------------- |
| Does **not** execute the file | Executes the file                 |
| Safe                          | Requires isolated sandbox/VM      |
| Faster                        | More time-consuming               |
| Looks at code and structure   | Observes runtime behavior         |
| CAPA is used here             | Sandboxes (Any.Run, Cuckoo, etc.) |


# Supported File Types

CAPA can analyze:

* Portable Executables (PE) (`.exe`, `.dll`)
* ELF binaries (Linux)
* .NET modules
* Shellcode
* Sandbox reports


-----------
