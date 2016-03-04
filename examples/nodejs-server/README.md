# A simple nodejs server based webchat

## Goal of this snap:
This snap illustrates how to snap a nodejs application as an app service. It's using the interface system to have access
to incoming network connection on its dedicated port.

## Notions:

* Packaging a nodejs application.
* Exposing it as a daemon and get access to its logs.
* Getting access to listening to the network for incoming connection.
* Plugin **nodejs**.

## Install and use it:

### Install from the store:
```sh
sudo snappy install nodejs-server-example
```

### Using it:

The nodejs app is daemonized when started. Point your browser to `http://<your-device-ip>:3000/` and start chatting!

You can check the daemon logs with:
```sh
sudo snappy service logs nodejs-server-example
```

## Technical notes

Thinks to note on this snap:
* We are using the [nodejs](../../docs/plugins.md) plugin, which is used to package nodejs application. This one refers
to `package.json` file and match through npm any needed dependencies, bundling them in the application.
* The application is exposed to the system as a daemon thanks to: `daemon: simple` which is part of the command stenza.
The nodejs server will start at system boot and stop on shutdown.
* We are asking access to the *network-listener* interface, getting the daemon being able to listen to incoming network
connection. This is done in 2 steps:
 * We define a `listener` slot, requesting access to the network-listener capability:
 ```
 slots:
   listener:
     interface: old-security
     caps: [network-listener]
```
 * We are giving access to this slot to our `webchat` application by defining `slots: [listener]`

## Further reading

Do not hesitate to check `snapcraft help nodejs` and `snapcraft help plugins` for more general informations.

If you are all new to Ubuntu Core and snapcraft, please hop on our [20 minutes developer guided tour](in-progress) to get started!

Also, feel free to refer to other [snapcraft examples](../) we have available for you!
