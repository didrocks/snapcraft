# A simple command line example using sl from ubuntu, with optimized snap size

## Goal of this snap:
This example illustrates the usage of a package taken from ubuntu and put in a snap where we only ship necessary files.
It's an extension of [this example](../deb-from-ubuntu/) explaining how to copy packages and dependencies from the
ubuntu archive. It uses snapcraft "snap" functionality to only pick some staged files part and ship them.
The uncompressed snap file is now 72K instead of 268K in the previous example (and 12K vs 40K for the snap itself)!

Finally, this example show how to export 2 commands wrapping `sl` and `sl-h`.

## Notions

* Filter staged content to reduce snap size.
* Export more than one command to the system.

## Install and use it:

### Install from the store:
```sh
sudo snappy install sl-light-example
```

### Using it:

Type on the command line:
```sh
sl-light-example.sl
```

or:
```sh
sl-light-example.sl-h
```

And enjoy the beautiful animations!

## Technical notes

* The filtering of files we want to ship from the current [parts](../../docs/snapcraft-parts.md) is done through the
**snap:** instruction. This one accept a list of files and regexp are also accepted, so we could have written, in a valid yaml format:

```
snap: [usr/games/sl*]
```
* We have **2 command stenzas** showing how to effectively export more than one command per snap.

## Further reading

If you look at the package content in `snap/` directory, you may find that shipping the man pages and LS are files that are unused is necessary. You can

Do not hesitate to check `snapcraft help nil` and `snapcraft help plugins` for more general informations.

If you are all new to Ubuntu Core and snapcraft, please hop on our [20 minutes developer guided tour](in-progress) to get started!

Also, feel free to refer to other [snapcraft examples](../README.md) we have available for you!
