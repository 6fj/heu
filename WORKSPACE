workspace(name = "com_alipay_sf_heu")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

### ref yasl ###
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

SECRETFLOW_GIT = "https://github.com/secretflow"

git_repository(
    name = "yasl",
    commit = "b50ed242ec17a28bff3274e5e6d152183d04ed8f",
    recursive_init_submodules = True,
    remote = "{}/yasl.git".format(SECRETFLOW_GIT),
)

load("@yasl//bazel:repositories.bzl", "yasl_deps")

yasl_deps()

#### fetch third-party deps ####

load("//third_party/bazel_cpp:repositories.bzl", "heu_cpp_deps")

heu_cpp_deps()

#### for cpp ####

load(
    "@rules_foreign_cc//foreign_cc:repositories.bzl",
    "rules_foreign_cc_dependencies",
)

rules_foreign_cc_dependencies(
    register_built_tools = False,
    register_default_tools = False,
    register_preinstalled_tools = True,
)

#### for python ####

http_archive(
    name = "rules_python",
    sha256 = "9fcf91dbcc31fde6d1edb15f117246d912c33c36f44cf681976bd886538deba6",
    strip_prefix = "rules_python-0.8.0",
    urls = [
        "https://github.com/bazelbuild/rules_python/archive/refs/tags/0.8.0.tar.gz",
    ],
)

# Python binding.
http_archive(
    name = "pybind11_bazel",
    sha256 = "a5666d950c3344a8b0d3892a88dc6b55c8e0c78764f9294e806d69213c03f19d",
    strip_prefix = "pybind11_bazel-26973c0ff320cb4b39e45bc3e4297b82bc3a6c09",
    urls = [
        "https://github.com/pybind/pybind11_bazel/archive/26973c0ff320cb4b39e45bc3e4297b82bc3a6c09.zip",
    ],
)

# We still require the pybind library.
http_archive(
    name = "pybind11",
    build_file = "@pybind11_bazel//:pybind11.BUILD",
    sha256 = "eacf582fa8f696227988d08cfc46121770823839fe9e301a20fbce67e7cd70ec",
    strip_prefix = "pybind11-2.10.0",
    urls = [
        "https://github.com/pybind/pybind11/archive/refs/tags/v2.10.0.tar.gz",
    ],
)

load("@pybind11_bazel//:python_configure.bzl", "python_configure")

python_configure(
    name = "local_config_python",
    python_version = "3",
)

#### for rust ####

http_archive(
    name = "rules_rust",
    sha256 = "29fee78077bd8c6477bc895a47e6c759f92df0735ed60587e1da7b51f53d26eb",
    strip_prefix = "rules_rust-23a4631cad819003642b1a148e458fe4ed2c54e1",
    urls = [
        # Main branch as of 2021-12-07
        "https://github.com/bazelbuild/rules_rust/archive/23a4631cad819003642b1a148e458fe4ed2c54e1.tar.gz",
    ],
)

load("@rules_rust//rust:repositories.bzl", "rust_repositories")

rust_repositories(version = "1.58.1")

load("//third_party/bazel_rust/cargo:crates.bzl", "rust_fetch_remote_crates")

rust_fetch_remote_crates()
