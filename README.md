
I've been trying to use the [podman-api](https://crates.io/crates/podman-api) crate in a Bazel workspace by using [rules_rust](https://github.com/bazelbuild/rules_rust) but lots of building errors occurred by just importing it.

To recreate the problem, open this repo inside a [dev container](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) in vscode, and build with the bazelisk command:

```bash
bazelisk build //hello_podman_api
```

The errors seem to be related to how variables are been captured for formating within macros like `impl_opts_builder` and `impl_opts_required_builder`.
For example:

```
error: there is no argument named `params`
  --> external/crate_index__podman-api-0.10.0/src/opts/containers.rs:11:1
   |
11 | / impl_opts_builder!(url =>
12 | |     /// Adjust the list of returned containers with this options.
13 | |     ContainerList
14 | | );
   | |_^
   |
   = note: did you intend to capture a variable `params` from the surrounding scope?
   = note: to avoid ambiguity, `format_args!` cannot capture variables when the format string is expanded from a macro
   = note: this error originates in the macro `$crate::impl_url_serialize` which comes from the expansion of the macro `impl_opts_builder` (in Nightly builds, run with -Z macro-backtrace for more info)
```

```
error: there is no argument named `params`
  --> external/crate_index__podman-api-0.10.0/src/opts/images.rs:11:1
   |
11 | / impl_opts_required_builder!(url =>
12 | |     /// Adjust how an image is built.
13 | |     ImageBuild,
14 | |     ///
...  |
17 | |     path => "path"
18 | | );
   | |_^
   |
   = note: did you intend to capture a variable `params` from the surrounding scope?
   = note: to avoid ambiguity, `format_args!` cannot capture variables when the format string is expanded from a macro
   = note: this error originates in the macro `$crate::impl_url_serialize` which comes from the expansion of the macro `impl_opts_required_builder` (in Nightly builds, run with -Z macro-backtrace for more info)
```


