licenses(["notice"])

package(default_visibility = ["//visibility:public"])

cc_library(
    name = "jni",
    hdrs = [
        ":jni.h",
        ":jni_md.h",
    ],
    # The includes line is necessary to expose these as system headers. Be
    # careful not to overpopulate this directory.
    includes = ["."],
)

# Hacky workaround to expose <jni.h> headers in cc_library rules. The JNI
# headers are magically exposed to genrules, so we export the headers of
# interest from those genrules. See
# https://github.com/tensorflow/tensorflow/blob/5dfbeab6c01a5919324a94c0092d34e6be218c3d/tensorflow/java/src/main/native/BUILD#L51
genrule(
    name = "copy_jni_h",
    srcs = ["@bazel_tools//tools/jdk:jni_header"],
    outs = ["jni.h"],
    cmd = "cp -f $< $@",
)

genrule(
    name = "copy_jni_md_h",
    srcs = select({
        "//conditions:default": ["@bazel_tools//tools/jdk:jni_md_header-linux"],
    }),
    outs = ["jni_md.h"],
    cmd = "cp -f $< $@",
)
