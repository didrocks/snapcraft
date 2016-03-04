# A simple command line example using sl from ubuntu

## Goal of this snap:
This snap illustrates the usage of a package taken from ubuntu and put in a snap. It uses snapcraft "stage package"
functionality to download and copy the whole package content (and its dependencies not present in Ubuntu Core) to the
resulting snap. The `sl` command is wrapped and corresponds to the package functionality.

## Notions:

* Import a deb package and its dependencies from the ubuntu distribution.
* Export one command to the system.
* Plugin **nil**.

## Install and use it:

### Install from the store:
```sh
sudo snappy install sl-example
```

### Using it:

Type on the command line:
```sh
sl-example.sl
```

And enjoy the beautiful animation!

## Technical notes

This is a pretty standard minimal snap. Things to note though:
* We are using the [nil](../../docs/plugins.md) plugin, which, as the name infers, do nothing. It will ship all files
that are present in this [parts](../../docs/snapcraft-parts.md), which is in that case all files from the sl package
and its dependencies.
* We have **one command stenza** showing how to effectively export one command of this snap to the system.
* **stage-packages: [sl]**:
 * This instruction ask for installing the **sl** package and all its dependencies not present in Ubuntu Core, in the
current parts it's in.
 * Note that it can be associated with any kind of plugins, and so, the effect can be combined with
other plugins effects, like filtering the list of files to ship, adding some build process, and so on.
* stage-packages accepts a list of packages, so this is equivalent to, in a valid yaml format:
```
stage-packages:
 - sl
```

## Further reading

If you look at the package content in `snap/` directory, you may find that we are shipping the man pages and LS which
aren't used. You can see how you can easily filter the files you ship from your parts
in [this examples](../filter-snap-content/).

Do not hesitate to check `snapcraft help nil` and `snapcraft help plugins` for more general informations.

If you are all new to Ubuntu Core and snapcraft, please hop on our [20 minutes developer guided tour](in-progress) to get started!

Also, feel free to refer to other [snapcraft examples](../) we have available for you!
