workspace(
    name = "jvolkman_rules_pycross",
)

load(":internal_deps.bzl", "rules_pycross_internal_deps")

# Fetch deps needed only locally for development
rules_pycross_internal_deps()

load("@rules_python//python/pip_install:repositories.bzl", "pip_install_dependencies")
pip_install_dependencies()

load("//pycross:repositories.bzl", "rules_pycross_dependencies")

# Fetch dependencies which users need as well
rules_pycross_dependencies()

# This pip_parse repo is only used to generate the pycross/private/pypi_requirements.bzl
load("@rules_python//python:pip.bzl", "pip_parse")
pip_parse(
    name = "rules_pycross_pypi_deps",
    requirements_lock = "//pycross/private:requirements.txt",
)

# For running our own unit tests
load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

bazel_skylib_workspace()

############################################
# Gazelle, for generating bzl_library targets
load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

go_rules_dependencies()

go_register_toolchains(version = "1.17.2")

gazelle_dependencies()
