cc_library(
    name = "main-jni-lib",
    srcs = [
        "Main.cc",
        "@local_jdk//:jni_header",
        "@local_jdk//:jni_md_header-linux",
    ],
    hdrs = ["Main.h"],
    include_prefix = "subfolder",
    includes = [
        "external/local_jdk/include",
        "external/local_jdk/include/linux",
    ],
)

genrule(
    name = "copy_jni_h",
    srcs = ["@bazel_tools//tools/jdk:jni_header"],
    outs = ["jni.h"],
    cmd = "cp -f $< $@",
)

genrule(
    name = "copy_jni_md_h",
    srcs = ["@bazel_tools//tools/jdk:jni_md_header-linux"],
    outs = ["jni_md.h"],
    cmd = "cp -f $< $@",
)

cc_library(
    name = "main-jni-lib2",
    srcs = [
        "Main.cc",
        ":jni.h",
        ":jni_md.h",
    ],
    hdrs = [
        "Main.h",
        ":jni.h",
        ":jni_md.h",
    ],
    linkopts = [
        "-lm",
        "-ldl",
    ],
    alwayslink = 1,
)

cc_binary(
    name = "libmain-jni.so",
    linkshared = 1,
    deps = [":main-jni-lib"],
)

java_binary(
    name = "Main",
    srcs = ["Main.java"],
    data = [":libmain-jni.so"],
    jvm_flags = ["-Djava.library.path=."],
    main_class = "Main",
)
