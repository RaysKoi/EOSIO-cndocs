# http_plugin插件

## 描述

`http_plugin`插件是`nodeos`和`keosd`均支持的核心插件。该插件为`nodeos`和`keosd`提供RPC API功能启用。

## 使用

```console
# config.ini
plugin = eosio::http_plugin
[options]
```

```sh
# command-line
nodeos ... --plugin eosio::http_plugin [options]
 (or)
keosd ... --plugin eosio::http_plugin [options]
```

## 选项


下列选项可以从`nodeos`和`keosd`命令行指定，也可以配置在`config.ini`文件中：

```console
Config Options for eosio::http_plugin:
  --unix-socket-path arg                The filename (relative to data-dir) to 
                                        create a unix socket for HTTP RPC; set 
                                        blank to disable (=keosd.sock for keosd)
  --http-server-address arg (=127.0.0.1:8888 for nodeos)
                                        The local IP and port to listen for 
                                        incoming http connections; set blank to
                                        disable.
  --https-server-address arg            The local IP and port to listen for 
                                        incoming https connections; leave blank
                                        to disable.
  --https-certificate-chain-file arg    Filename with the certificate chain to 
                                        present on https connections. PEM 
                                        format. Required for https.
  --https-private-key-file arg          Filename with https private key in PEM 
                                        format. Required for https
  --https-ecdh-curve arg (=secp384r1)   Configure https ECDH curve to use: 
                                        secp384r1 or prime256v1
  --access-control-allow-origin arg     Specify the Access-Control-Allow-Origin
                                        to be returned on each request.
  --access-control-allow-headers arg    Specify the Access-Control-Allow-Header
                                        s to be returned on each request.
  --access-control-max-age arg          Specify the Access-Control-Max-Age to 
                                        be returned on each request.
  --access-control-allow-credentials    Specify if Access-Control-Allow-Credent
                                        ials: true should be returned on each 
                                        request.
  --max-body-size arg (=1048576)        The maximum body size in bytes allowed 
                                        for incoming RPC requests
  --http-max-bytes-in-flight-mb arg (=500)
                                        Maximum size in megabytes http_plugin 
                                        should use for processing http 
                                        requests. 503 error response when 
                                        exceeded.
  --verbose-http-errors                 Append the error log to HTTP responses
  --http-validate-host arg (=1)         If set to false, then any incoming 
                                        "Host" header is considered valid
  --http-alias arg                      Additionaly acceptable values for the 
                                        "Host" header of incoming HTTP 
                                        requests, can be specified multiple 
                                        times.  Includes http/s_server_address 
                                        by default.
  --http-threads arg (=2)               Number of worker threads in http thread
                                        pool
```

## 依赖关系

无
