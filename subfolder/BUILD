cc_library(
    name = "main-jni-lib",
    srcs = [
        "Main.cc",
        "@local_jdk//:jni_header",
        "@local_jdk//:jni_md_header-linux",
    ],
    hdrs = ["Main.h"],
    includes = [
        "external/local_jdk/include",
        "external/local_jdk/include/linux",
    ],
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
