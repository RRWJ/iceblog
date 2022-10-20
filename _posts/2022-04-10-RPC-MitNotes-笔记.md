---
layout: post
title: RPC MitNote 笔记
subtitle: rpc
date: 2022-04-10
tags: [Go][rpc][MIT6.824]
comments: false
---

# Remote Procedure Call (RPC)
```
  1. a key piece of distributed system machinery;all the labs use RPC
  2. goal: easy-to-program client/server communication
  3. hide details of network protocols
  4. convert data (strings, arrays, maps, &c) to "wire format"
  5. portability / interoperability
```
### RPC message diagram:
```
  Client             Server
    request--->
       <---response
```
### Software structure
```
  client app        handler fns
   stub fns         dispatcher
   RPC lib           RPC lib
     net  ------------ net
```
### Go example: kv.go on schedule page
```
  A toy key/value storage server -- Put(key,value), Get(key)->value
  Uses Go's RPC library
  Common:
    Declare Args and Reply struct for each server handler.
  Client:
    connect()'s Dial() creates a TCP connection to the server
    get() and put() are client "stubs"
    Call() asks the RPC library to perform the call
      you specify server function name, arguments, place to put reply
      library marshalls args, sends request, waits, unmarshalls reply
      return value from Call() indicates whether it got a reply
      usually you'll also have a reply.Err indicating service-level failure
  Server:
    Go requires server to declare an object with methods as RPC handlers
    Server then registers that object with the RPC library
    Server accepts TCP connections, gives them to RPC library
    The RPC library
      reads each request
      creates a new goroutine for this request
      unmarshalls request
      looks up the named object (in table create by Register())
      calls the object's named method (dispatch)
      marshalls reply
      writes reply on TCP connection
    The server's Get() and Put() handlers
      Must lock, since RPC library creates a new goroutine for each request
      read args; modify reply
```
### A few details:
```
  1. Binding: how does client know what server computer to talk to?
    For Go's RPC, server name/port is an argument to Dial
    Big systems have some kind of name or configuration server
  2. Marshalling: format data into packets
    Go's RPC library can pass strings, arrays, objects, maps, &c
    Go passes pointers by copying the pointed-to data
    Cannot pass channels or functions
```
### RPC problem: what to do about failures?
```
  e.g. lost packet, broken network, slow server, crashed server
```
### What does a failure look like to the client RPC library?
```
  Client never sees a response from the server
  Client does *not* know if the server saw the request!
    [diagram of losses at various points]
    Maybe server never saw the request
    Maybe server executed, crashed just before sending reply
    Maybe server executed, but network died just before delivering reply
```
### Simplest failure-handling scheme: "best-effort RPC"
```
  Call() waits for response for a while
  If none arrives, re-send the request
  Do this a few times
  Then give up and return an error
```
### Q: is "best effort" easy for applications to cope with?
```
A particularly bad situation:
  client executes
    Put("k", 10);
    Put("k", 20);
  both succeed
  what will Get("k") yield?
  [diagram, timeout, re-send, original arrives late]
```

### Q: is best effort ever OK?
```
   read-only operations
   operations that do nothing if repeated
     e.g. DB checks if record has already been inserted
```
### Better RPC behavior: "at-most-once RPC"
```
  idea: client re-sends if no answer;
    server RPC code detects duplicate requests,
    returns previous reply instead of re-running handler
  Q: how to detect a duplicate request?
  client includes unique ID (XID) with each request
    uses same XID for re-send
  server:
    if seen[xid]:
      r = old[xid]
    else
      r = handler()
      old[xid] = r
      seen[xid] = true
```
### some at-most-once complexities
```
  this will come up in lab 3
  what if two clients use the same XID?
    big random number?
  how to avoid a huge seen[xid] table?
    idea:
      each client has a unique ID (perhaps a big random number)
      per-client RPC sequence numbers
      client includes "seen all replies <= X" with every RPC
      much like TCP sequence #s and acks
    then server can keep O(# clients) state, rather than O(# XIDs)
  server must eventually discard info about old RPCs or old clients
    when is discard safe?
  how to handle dup req while original is still executing?
    server doesn't know reply yet
    idea: "pending" flag per executing RPC; wait or ignore
```
### What if an at-most-once server crashes and re-starts?
```
  if at-most-once duplicate info in memory, server will forget
    and accept duplicate requests after re-start
  maybe it should write the duplicate info to disk
  maybe replica server should also replicate duplicate info
```
### Go RPC is a simple form of "at-most-once"
```
  open TCP connection
  write request to TCP connection
  Go RPC never re-sends a request
    So server won't see duplicate requests
  Go RPC code returns an error if it doesn't get a reply
    perhaps after a timeout (from TCP)
    perhaps server didn't see request
    perhaps server processed request but server/net failed before reply came back
```