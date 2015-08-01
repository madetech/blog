# Stream everything

> This is the Unix philosophy: Write programs that do one thing and do it well. Write programs to work together. Write programs to handle text streams, because that is a universal interface. - _Doug McIlroy, inventor of Unix pipes_

### What are Streams?

'Streams' and 'pipes' have been an essential part of \*nix systems since the 1970s, when Doug McIlroy introduced them into the first version of Unix. The story goes that he threatened to leave the project if they weren't implemented, he felt so strongly that they were a cornerstone of an effective modular operating system, and key to interoperability. They facilitate the Unix philosophies of 'do one thing and one thing well' and 'write programs that speak to other programs.' A small Unix program like `cat`, which concatenates the contents of one or more files and prints out the buffer, is able to communicate with other programs through piping. You could `cat` a file containing a list of words, pipe that to a sorting program, and then finally to a text file. You could write this complex operation more simply than you could explain it.

```shell
cat names.txt | sort  > output.txt
```

Despite its long time popularity at the Operating System level, I'm sure you've written app code like the following. Everyone has.

```javascript
import { readFile } from 'fs';

readFile('./document.txt', function(err, buffer) {
  let lines = buffer.toString().split(/\n/);
  lines.forEach(function(line) {
    if(line.includes('test')) {
      console.log(line);
    }
  });
});
```

The issue with this is you have to load the entire `document.txt` file into memory, split it on every line, and print each out one by one. This introduces a huge overhead on a simple operation, and cannot scale. A 500MB GeoJSON file would ruin your app. Not only would it take up a huge amount of memory, but it would take 10 minutes to load. Writing inefficient code like this on the shell actually takes more work, because the technique of piping streams around is so deeply embedded. We would write it like this:

```shell
cat document.txt | grep 'test'
```

Simple and readable. Here, input will start flowing through each program, one by one, immediately. Each program receives a chunk of data, can choose to modify it and pass it along, or ignore it completely, then waits for the next chunk of data.

The ideal way to write app code in Node.js can mirror this. If you substitute `cat` and `grep` with the [fs][node_fs] module in Node's standard library and a custom stream you have essentially the same code.

You could write a simple function which returns a 'grep' stream using a module like [through][npm_through].

```javascript
function grep(word) {
  return through(function(line) {
    // This function receives every chunk of data.
    if(line.includes(word)) {
      // Pass it to the next stream if it matches the word.
      this.write(line);
    }
  });
}
```

And then put it to work.

```javascript
fs.createReadStream('./document.txt')
  .pipe(grep('test'))
  .pipe(process.stdout);
```

Why would it need to change? Text streams were designed to be the "universal interface" by which all programs interacted with each other. A large amount of Node.js's standard library revolves around the use of streams. They have incredible composability. You can make an HTTP request and pipe its response directly to a text file, or to a remote party. For example, the most basic proxy server could look like this:

```javascript
app.get('/:url', function(req, response) {
  // httprequest is returning a readable stream, which
  // is piped directly to a writable stream ('response'.)
  httprequest(req.params.url).pipe(response);
});
```

This technique obviously isn't limited to the shell and Node.js - many languages support Streams to varying degrees. The reason Node's implementation is particularly successful is because it has been integrated with most of its standard library. This means the canonical _best_ way to do most basic operations involves using a stream to do so. For example, reading and writing files, making HTTP requests or sending data to a client.

### DOMNode

One of the more interesting applications of Streams is using them in the browser.

DOMNode is a library which brings Node concepts and functionality to the browser. It uses [browserify][npm_browserify] to wrap up Node standard modules where possible, and polyfills where not. For example, it allows you to use the `events` library straight from the Node source, or a browser specific `fs` library.

Better still, it provides Node style replacements or extensions to browser specific operations. For example, it allows you to use Streams when making XHR requests or using websocket connections.

```javascript
import http from 'http-browserify';
import websocket from 'websocket-stream';

// The following are both streams
let httpStream = http.request({ method: 'POST', host: '/' });
let wsStream = websocket('ws://localhost');
```

A really interesting interface included in DOMnode is its streaming geolocation API.

```javascript
import geolocation from 'geolocation-stream';

// Create a movement stream
let movement = geolocation();

// Every time data (movement) is made, log it.
movement.on('data', function(location) {
  console.log(location);
});
```

Again, this is more than just an event emitter. This movement stream could be piped to any other stream. For a slightly unnerving example, you could pipe all movements to a server, and write those to a JSON file.

In the browser:

```javascript
// Every time movement is made, pipe its data to the websocket.
movement.pipe(wsStream);
```

On the server:

```javascript
// Using a different websocket implementation, receive data through
// a websocket as a stream. Pipe its data to a text file.
websocket.createServer({ server: app }, function(stream) {
  let file = fs.createWriteStream('geo-data.json');
  stream.pipe(json()).pipe(file);
});
```

Streams are essential technology. Not only do they have incredible composability, interoperability and reability, but they have real technical merit. They don't make you wait. Data is piped from stream to stream as it comes, not after it has buffered in each. This is critical for large amounts of data, but effective even for small amounts of data. We spend a lot of time optimising code for speed and efficiency, but ignore the channels by which our primary concern - data - is passed around our applications.

In Ruby, for example, slow operations like file reads or Net requests are too frequently handled synchronously, blocking the rest of the app. Although Ruby _does_ have streaming operations, they should be simpler to use and be included in more of the standard library. They are fundamental in Node because they are key to the OS running underneath. They should be that way in all languages.

#### Further reading

- [Stream handbook](https://github.com/substack/stream-handbook)
- [Harnessing The Awesome Power Of Streams (LXJS 2012)](https://www.youtube.com/watch?v=lQAV3bPOYHo)
- [Basics of the UNIX Philosophy](http://www.faqs.org/docs/artu/ch01s06.html)

[node_fs]: https://nodejs.org/api/fs.html
[npm_through]: https://www.npmjs.com/package/through
[npm_browserify]: https://www.npmjs.com/package/browserify
