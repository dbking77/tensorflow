# Description:
# TensorFlow Lite Example Label Image.

load("//tensorflow/lite:build_def.bzl", "tflite_linkopts")

package(
    default_visibility = ["//visibility:public"],
)

cc_binary(
    name = "run_detector",
    srcs = [
        "run_detector.cpp",
    ],
    linkopts = tflite_linkopts() + select({
        "//tensorflow:android": [
            "-pie",  # Android 5.0 and later supports only PIE
            "-lm",  # some builtin ops, e.g., tanh, need -lm
            "-Wl,-rpath=/data/local/tmp",  # for hexagon delegate
        ],
        "//conditions:default": [],
    }),
    deps = [
        #":bitmap_helpers",
        "//tensorflow/lite:framework",
        #"//tensorflow/lite:string_util",
        #"//tensorflow/lite/delegates/nnapi:nnapi_delegate",
        "//tensorflow/lite/kernels:builtin_ops",
        #"//tensorflow/lite/profiling:profiler",
        #"//tensorflow/lite/tools/evaluation:utils",
        #"@com_google_absl//absl/memory",
    ] + select({
        "//tensorflow:android": [
            "//tensorflow/lite/delegates/gpu:gl_delegate",
            "//tensorflow/lite/experimental/delegates/hexagon:hexagon_delegate",
        ],
        "//tensorflow:android_arm64": [
            "//tensorflow/lite/delegates/gpu:gl_delegate",
            "//tensorflow/lite/experimental/delegates/hexagon:hexagon_delegate",
        ],
        "//conditions:default": [],
    }),
)


# cc_binary(
#     name = "run_detector",
#     srcs = ["run_detector.cpp"],
#     deps = [
#         "//tensorflow/lite:tensorflowlite",
#         #"//tensorflow/core:tensorflow",
#         #"@tensorflow//tensorflow/lite:tensorflow",
#         #"//tensorflow/core:tensorflow",
#     ]
# )
