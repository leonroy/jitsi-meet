# Jitsi Meet Development

## Enable Chrome accept self signed

In address bar:

    chrome://flags/#allow-insecure-localhost

## Run jitsi-meet

Specify your Jitsi Meet Server running http-bind etc.

    export WEBPACK_DEV_SERVER_PROXY_TARGET=https://barev.brring.com

Build and run Jitsi Meet:

    npm install
    make dev

Visit *https://localhost:8080*

## Further Install notes

https://jitsi.org/news/tag/tutorial/
