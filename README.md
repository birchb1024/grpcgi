# grpcgi (an IDEA)
Universally generic gRPC server with a common gateway intyerface which forks sub-processes.    

# Description
*This is just an idea today.* 

The goal is to allow very rapid development of gRPC services including leveraging existing command-line programs. It's a way to rapidly hack prototypes. It can be used in production if all the usual good practices are applied.
A sub-goal is to provide a way to mock or emulate gRPC services for use in testing scenarios. A sub-sub goal is for it to work well with [grpcurl](https://github.com/fullstorydev/grpcurl) A sub³ goal is to work with these languages: Standard ML, Python, Lua, Go, JavaScript but not Java or COBOL. A sub⁴ goal is to embed an interpreter like [golua](https://github.com/arnodel/golua) or better.

grpci will work like [grpcmock](https://github.com/tokopedia/gripmock) and [terraform-provider-universe](https://github.com/birchb1024/terraform-provider-universe)
- it is a standalone gRPC server written in (maybe) Go
- it reads proto files locally to define the services and datatypes provided
- it has reflection enabled so clients can auto-discover services and types
- when a method request is received it is converted to JSON, a seperate process is invoked a la [CGI](https://en.wikipedia.org/wiki/Common_Gateway_Interface). The request JSON is given on the process' stdin, the process executes and its response is returned to grpcgi in JSON format. The response is converted and transmitted to the client.
- the binding between the service and the sub-process executable is TBD but may be as simple as the exe name must match the service name. 

# Synopsis

```
grpcgi [options] <hostname>:<port> <list of paths to executable directories ($PATH is not used)> <path to proto directory>... 
```


# Undecided
_This section is about design elements up in the air_
- Whether to be compatible with the actual CGI standard

# Footnotes
Unlike [grpcmock](https://github.com/tokopedia/gripmock) there is no stored responses, matching or uploading via HTTP.
