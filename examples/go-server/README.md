# A simple go webserver example

## Goal of this snap:
This snap illustrates how to snap a go application as an app service. It's using the interface system to have access
to incoming network connection on its dedicated port.
We take the source code from an external git repository and use a subdirectory of it.

## Notions:

* Packaging a go application.
* Exposing it as a daemon and get access to its logs.
* Getting the source code trough an external repository.
* Getting access to listening to the network for incoming connection.
* Plugin **go**.

## Install and use it:

### Install from the store:
```sh
sudo snappy install go-server-example
```

### Using it:

The go app is daemonized when started. Point your browser to `http://<your-device-ip>:8080/` and start browsing
pictures.

You can check the daemon logs with:
```sh
sudo snappy service logs go-server-example
```

## Technical notes

Thinks to note on this snap:
* We are using the [go](../../docs/plugins.md) plugin, which is used to package go application. This one will run
`go get` to fetch any needed dependencies, build and bundling them in the application.
* The application is exposed to the system as a daemon thanks to: `daemon: simple` which is part of the command stenza.
The go server will start at system boot and stop on shutdown.
* We are getting access to an external git repository to branch the source code using `source: <url>`. Note that we
may have to specify which VCS is in use when automatic detection can't determine which one to use. We can as well
specify which subdirectories are interesting to us.
* We are asking access to the *network-listener* interface, getting the daemon being able to listen to incoming network
connection. This is done in 2 steps:
 * We define a `listener` slot, requesting access to the network-listener capability:
 ```
 slots:
   listener:
     interface: old-security
     caps: [network-listener]
```
 * We are giving access to this slot to our `goserver` application by defining `slots: [listener]`


## Further reading

Do not hesitate to check `snapcraft help go`, `snapcraft help sources` and `snapcraft help plugins` for more general
informations.

If you are all new to Ubuntu Core and snapcraft, please hop on our [20 minutes developer guided tour](in-progress) to get started!

Also, feel free to refer to other [snapcraft examples](../README.md) we have available for you!
