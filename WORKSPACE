workspace(name = "hello_world")


load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_rust",
    sha256 = "950a3ad4166ae60c8ccd628d1a8e64396106e7f98361ebe91b0bcfe60d8e4b60",
    urls = ["https://github.com/bazelbuild/rules_rust/releases/download/0.20.0/rules_rust-v0.20.0.tar.gz"],
)

load("@rules_rust//rust:repositories.bzl", "rules_rust_dependencies", "rust_register_toolchains")

rules_rust_dependencies()

rust_version = "1.69.0"

rust_register_toolchains(
    edition = "2021",
    versions = [rust_version],
)

load("@rules_rust//crate_universe:repositories.bzl", "crate_universe_dependencies")

crate_universe_dependencies(bootstrap = True)

load("@rules_rust//crate_universe:defs.bzl", "crate", "crates_repository")

crates_repository(
    name = "crate_index",
    cargo_lockfile = "//:Cargo.lock",
    lockfile = "//:Cargo.bazel.lock",
    packages = {
        "base64": crate.spec(version = "0.13.1"),
        "byteorder": crate.spec(version = "1.4.3"),
        "bytes": crate.spec(version = "1.4.0"),
        "chrono": crate.spec(version = "0.4.24"),
        # "containers-api": crate.spec(version = "0.8.0"),
        "containers-api": crate.spec(
            git = "https://github.com/vv9k/containers-api.git",
            branch = "master",
        ),
        "flate2": crate.spec(version = "1.0.26"),
        "futures-util": crate.spec(version = "0.3.28"),
        "futures_codec": crate.spec(version = "0.4.1"),
        "log": crate.spec(version = "0.4.17"),
        "paste": crate.spec(version = "1.0.12"),
        "podman-api-stubs": crate.spec(version = "0.9.0"),
        "serde": crate.spec(version = "1.0.160", features = ["derive"]),
        "serde_json": crate.spec(version = "1.0.96"),
        "tar": crate.spec(version = "0.4.38"),
        "thiserror": crate.spec(version = "1.0.40"),
        "tokio": crate.spec(version = "1.28.0"),
        "url": crate.spec(version = "2.3.1"),
    },
)

http_archive(
    name = "crate_podman_api",
    build_file = "//third_party/crate_podman_api:BUILD.podman_api.bazel",
    # sha256 = "146b6b46b9babcb9bb8dcf9e3614d7f9b649b7d37315d568e90c312c88792f30",
    # strip_prefix = "podman-api-rs-0.10.0",
    # urls = ['https://github.com/vv9k/podman-api-rs/archive/refs/tags/0.10.0.zip']
    sha256 = "62e28c9db1d9b4e18bff9c2784205759095effd53ecc9d503e73f975ecc679c7",
    strip_prefix = "podman-api-rs-f35e6f9f9fdb9d9023aed341252c16c0ad9796d1",
    urls = ["https://github.com/vv9k/podman-api-rs/archive/f35e6f9f9fdb9d9023aed341252c16c0ad9796d1.zip"],


)

load("@crate_index//:defs.bzl", "crate_repositories")

crate_repositories()
