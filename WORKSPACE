workspace(
    name = "repro",
    managed_directories = {"@npm": ["node_modules"]},
)

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# https://github.com/bazelbuild/rules_nodejs/releases

# yarn build works fine
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "b3521b29c7cb0c47a1a735cce7e7e811a4f80d8e3720cf3a1b624533e4bb7cb6",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/2.3.2/rules_nodejs-2.3.2.tar.gz"],
)

# yarn build times out
# http_archive(
#     name = "build_bazel_rules_nodejs",
#     sha256 = "6142e9586162b179fdd570a55e50d1332e7d9c030efd853453438d607569721d",
#     urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/3.0.0/rules_nodejs-3.0.0.tar.gz"],
# )

load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")

yarn_install(
    name = "npm",
    package_json = "//:package.json",
    quiet = False,
    yarn_lock = "//:yarn.lock",
)

# https://github.com/bazelbuild/rules_sass#setup
http_archive(
    name = "io_bazel_rules_sass",
    sha256 = "9dcfba04e4af896626f4760d866f895ea4291bc30bf7287887cefcf4707b6a62",
    strip_prefix = "rules_sass-1.26.3",
    url = "https://github.com/bazelbuild/rules_sass/archive/1.26.3.zip",
)

load("@io_bazel_rules_sass//:package.bzl", "rules_sass_dependencies")

rules_sass_dependencies()

load("@io_bazel_rules_sass//:defs.bzl", "sass_repositories")

sass_repositories()
