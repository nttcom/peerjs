# Deprecated!

We have released a new WebRTC platform, [ECLWebRTC](https://webrtc.ecl.ntt.com/en/?origin=skyway), to take the place of SkyWay. We will be shutting down the SkyWay servers in March 2018. Customers who are currently using SkyWay are required to migrate to ECLWebRTC by then or their services will stop working.

If you are looking for the repository of ECLWebRTC, please see the [new JavaScript SDK](https://github.com/skyway/skyway-js-sdk).

このレポジトリは、2018年3月に提供を終了する旧SkyWayのJavaScript SDKです。[新しいSkyWay](https://webrtc.ecl.ntt.com/?origin=skyway)への移行をお願いします。

すでに新しいSkyWayをご利用の方は、[新しいJavaScript SDK](https://github.com/skyway/skyway-js-sdk)をご覧ください。

# PeerJS: Simple peer-to-peer with WebRTC #

PeerJS provides a complete, configurable, and easy-to-use peer-to-peer API built on top of WebRTC, supporting both data channels and media streams.

## Notice 
This branch is a customized version of PeerJS for NTT Communications's WebRTC platform SkyWay.
- [http://nttcom.github.io/skyway](http://nttcom.github.io/skyway/en)

## Setup


**Include the library**

```html
<script src="https://skyway.io/dist/0.3/peer.js"></script>
```

**Include with NPM**

```
npm install skyway-peerjs
```

**Create a Peer**  
Get a [free API key](http://nttcom.github.io/skyway/registration.html). Your id only needs to be unique to the namespace of your API key.
```javascript
var peer = new Peer('pick-an-id', {key: 'myapikey'}); 
// You can pick your own id or omit the id if you want to get a random one from the server.
```

## Data connections
**Connect**
```javascript
var conn = peer.connect('another-peers-id');
conn.on('open', function(){
  conn.send('hi!');
});
```
**Receive**
```javascript
peer.on('connection', function(conn) {
  conn.on('data', function(data){
    // Will print 'hi!'
    console.log(data);
  });
});
```

## Media calls
**Call**
```javascript
navigator.getUserMedia = navigator.getUserMedia || navigator.webkitGetUserMedia || navigator.mozGetUserMedia;
navigator.getUserMedia({video: true, audio: true}, function(stream) {
  var call = peer.call('another-peers-id', stream);
  call.on('stream', function(remoteStream) {
    // Show stream in some <video> element.
  });
}, function(err) {
  console.log('Failed to get local stream' ,err);
});

```
**Answer**
```javascript
navigator.getUserMedia = navigator.getUserMedia || navigator.webkitGetUserMedia || navigator.mozGetUserMedia;
peer.on('call', function(call) {
  navigator.getUserMedia({video: true, audio: true}, function(stream) {
    call.answer(stream); // Answer the call with an A/V stream.
    call.on('stream', function(remoteStream) {
      // Show stream in some <video> element.
    });
  }, function(err) {
    console.log('Failed to get local stream' ,err);
  });
});
```

## SkyWay Links

### [Documentation / API Reference](http://nttcom.github.io/skyway/docs)

### [Changelog](https://github.com/nttcom/peerjs/blob/master/changelog.md)

### [free API key](http://nttcom.github.io/skyway/registration.html)

### [Discuss SkyWay on our Google Group](https://groups.google.com/forum/#!forum/skywayjs)

## PeerJS links

### [WebRTC Browser compatibility status](http://peerjs.com/status)

### [PeerServer](https://github.com/peers/peerjs-server)

### [Discuss PeerJS on our Google Group](https://groups.google.com/forum/?fromgroups#!forum/peerjs)


