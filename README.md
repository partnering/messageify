# HOW-TO use messageify

## overview

messageify assumes is a very thin layer on top of stream sockets (unix sockets, tcp sockets). It assumes that every message starts
with 4-bytes containing the length of the message in bytes, followed by the actual message.

## example

```js
const net = require('net')

let server = net.createServer(socket => {
  socket = messageify(socket)
  socket.on('message', message => {
    console.log(JSON.parse(message))
  })

  socket.sendMessage(JSON.stringify({ foo: "bar" }))
})

server.listen("/socket/path.sock")
```


