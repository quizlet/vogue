# Vogue

Vogue creates a real-time link between your web browser and your file system.
When you save a CSS file, used by the HTML page in your browser, Vogue will
make the browser reload the stylesheet. Only the stylesheet is reloaded, not the
entire page, making it work even for very dynamic/ajax pages.

Vogue is all javascript. It runs a server on [Node.js](http://nodejs.org/),
which will watch the file system.
The server accepts WebSocket connections from the Vogue client code
(which uses [socket.io](http://socket.io/)).
The client javascript can be loaded into a HTML page using a single script tag.

## Usage
Run the Vogue server.

    vogue /path/to/website

Multiple directories can be watched by separating the paths with colons.
(e.g. `vogue /path/to/website:/path/to/second/website`.)

SSL pages are also supported, but a valid certificate must be provided (see
options).

### Options
See all options with `vogue --help`.

* `--port`, `-p`: Port to run the Vogue server on (HTTP). Defaults to 8001.
* `--ssl_port`, `-s`: Port to run the Vogue server on (HTTPS). Defaults to 8002.
* `--key`, `-k`: An optional private key file (`.pem` or `.key` format).
* `--cert`, `-c`: An optional certificate file (`.pem` or `.crt` format).
* `--ca`, `-a`: An optional intermediate certificate file (`.pem` or `.crt` format).
* `--refresh`, `-t`: Number of milliseconds between checking for new files in the file tree. Defaults to 20000 (20 seconds).

## Demo
Vogue runs a separate HTTP server from the one running your website.
To run the Vogue demo, do the following:

    cd demo
    python -m SimpleHTTPServer

Then, from another terminal session, run Vogue:

    vogue demo

Open http://localhost:8000 (or the port used by your web server)
to view the demo. The demo page has the Vogue client javascript
already included. It will connect to the Vogue server, which watches the two 
CSS files in the `demo/styles` directory.

Try editing the CSS files in the `demo/styles` directory. When you save, you
will see a blue dot appear and turn yellow once the page updates to reflect the
changes made. This is done without reloading the entire page.

Copyright &copy; 2011 Andrew Davey (andrew@equin.co.uk)
