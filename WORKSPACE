workspace(
    name = "repro",
    managed_directories = {"@npm": ["node_modules"]},
)

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# https://github.com/bazelbuild/rules_nodejs/releases

# yarn build works fine
# http_archive(
#     name = "build_bazel_rules_nodejs",
#     sha256 = "b3521b29c7cb0c47a1a735cce7e7e811a4f80d8e3720cf3a1b624533e4bb7cb6",
#     urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/2.3.2/rules_nodejs-2.3.2.tar.gz"],
# )

# yarn build times out
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "6142e9586162b179fdd570a55e50d1332e7d9c030efd853453438d607569721d",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/3.0.0/rules_nodejs-3.0.0.tar.gz"],
)

# Fetch sass rules for compiling sass files
http_archive(
    name = "io_bazel_rules_sass",
    patch_args = ["-p1"],
    # We need the latest rules_sass to get the --bazel_patch_module_resolver behavior
    # However it seems to have a bug, so we patch back to the prior dart-sass version.
    # See https://github.com/bazelbuild/rules_sass/issues/127
    # TODO(alexeagle): fix upstream and remove patch
    patches = ["@build_bazel_rules_nodejs//:rules_sass.issue127.patch"],
    sha256 = "8392cf8910db2b1dc3b488ea18113bfe4fd666037bf8ec30d2a3f08fc602a6d8",
    strip_prefix = "rules_sass-1.30.0",
    urls = [
        "https://github.com/bazelbuild/rules_sass/archive/1.30.0.zip",
        "https://mirror.bazel.build/github.com/bazelbuild/rules_sass/archive/1.30.0.zip",
    ],
)

load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")

yarn_install(
    name = "npm",
    package_json = "//:package.json",
    quiet = False,
    yarn_lock = "//:yarn.lock",
)

# Setup the rules_sass toolchain
load("@io_bazel_rules_sass//sass:sass_repositories.bzl", "sass_repositories")

sass_repositories()
