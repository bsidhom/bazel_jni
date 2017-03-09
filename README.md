# Bazel JNI Helpers

This repository contains helper utilities for building JNI libraries with Bazel.

# How to use

In your `WORKSPACE` file, add the following:
```bazel
git_repository(
    name = "bazel_jni",
    remote = "https://github.com/bsidhom/bazel_jni.git",
    commit = "<commit hash>",
)
```
You can pull any commit hash from this repository.

To create a library that depends on JNI headers, add a dependency to
`@bazel_jni//third_party/jni`. For example:

```bazel
cc_binary(
    name = "libmy_jni_library.so",
    srcs = ["my_jni_library.cc"],
    deps = ["@bazel_jni//third_party/jni"],
    linkshared = 1,
)
```

You can then depend on this from a `java_*` rule as normal.
