IP API for Scala.js
================================
[ip](https://www.npmjs.com/package/ip) - IP address utilities for node.js.

### Description

IP address utilities for node.js

### Build Dependencies

* [SBT v0.13.13](http://www.scala-sbt.org/download.html)

### Build/publish the SDK locally

```bash
 $ sbt clean publish-local
```

### Running the tests

Before running the tests the first time, you must ensure the npm packages are installed:

```bash
$ npm install
```

Then you can run the tests:

```bash
$ sbt test
```

### Examples

```scala
import io.scalajs.nodejs.buffer.Buffer
import io.scalajs.npm.ip._
import scala.scalajs.js

IP.address() // my ip address
IP.isEqual("::1", "::0:1") // true
IP.toBuffer("127.0.0.1") // Buffer([127, 0, 0, 1])
IP.toString(new Buffer(js.Array(127, 0, 0, 1))) // 127.0.0.1
IP.fromPrefixLen(24) // 255.255.255.0
IP.mask("192.168.1.134", "255.255.255.0") // 192.168.1.0
IP.cidr("192.168.1.134/26") // 192.168.1.128
IP.not("255.255.255.0") // 0.0.0.255
IP.or("192.168.1.134", "0.0.0.255") // 192.168.1.255
IP.isPrivate("127.0.0.1") // true
IP.isV4Format("127.0.0.1") // true
IP.isV6Format("::ffff:127.0.0.1") // true

// operate on buffers in-place 
val buf = new Buffer(128)
val offset = 64
IP.toBuffer("127.0.0.1", buf, offset)  // [127, 0, 0, 1] at offset 64
IP.toString(buf, offset, 4)            // "127.0.0.1"
 
// subnet information 
IP.subnet("192.168.1.134", "255.255.255.192")
// { networkAddress: "192.168.1.128", 
//   firstAddress: "192.168.1.129", 
//   lastAddress: "192.168.1.190", 
//   broadcastAddress: "192.168.1.191", 
//   subnetMask: "255.255.255.192", 
//   subnetMaskLength: 26, 
//   numHosts: 62, 
//   length: 64, 
//   contains: function(addr){...} } 

IP.cidrSubnet("192.168.1.134/26")
// Same as previous. 
 
// range checking 
IP.cidrSubnet("192.168.1.134/26").contains("192.168.1.190") // true 
```

### Artifacts and Resolvers

To add the `IP` binding to your project, add the following to your build.sbt:  

```sbt
libraryDependencies += "io.scalajs.npm" %%% "ip" % "0.4.0-pre4"
```

Optionally, you may add the Sonatype Repository resolver:

```sbt   
resolvers += Resolver.sonatypeRepo("releases") 
```