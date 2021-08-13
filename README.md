# operator-manifest-tools
Tooling that enables software release pipelines for operator manifests.

## Commands

Command documentation: [Operator Manifest Tools](docs/operator-manifest-tools.md).

``` sh
Usage:
  operator-manifest-tools [command]

Available Commands:
  completion  generate the autocompletion script for the specified shell
  help        Help about any command
  pinning     Operator manifest image pinning

Flags:
  -h, --help      help for operator-manifest-tools
  -v, --verbose   Print debug output of the command

Use "operator-manifest-tools [command] --help" for more information about a command.
```

### Pinning

#### Usage

The pinning subcommands are meant to **extract** a ClusterServiceVersion yaml file in a directory, **resolve** the images tags to a digest, and **replace** the image references with tags to images with digests.

The 3 subcommands can be done at one time using the **pin** command. It is also possible to string the **extract**, **resolve**, and **replace** commands together using Unix/Linux pipes.

Example:

``` sh
# pin a csv in a directory
operator-manifest-tools pinning pin $MANIFEST_DIR

# equalivent to pin; doesn't generate temporary files for the cmd though
operator-manifest-tools pinning extract $MANIFEST_DIR - | operator-manifest-tools pinning resolve - | operator-manifest-tools pinning replace $MANIFEST_DIR
```

#### Custom Resolve Scripts

It's possible to replace skopeo with other resolve mechanisms (i.e. docker). The resolve and pin command can take parameters that will override the skopeo default with a script. Please see [hack/resolvers/skopeo.sh](hack/resolvers/skopeo.sh) for an example using skopeo.
