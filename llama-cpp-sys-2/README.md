# llama-cpp-sys

Raw bindings to llama.cpp with cuda support.

See [llama-cpp-2](https://crates.io/crates/llama-cpp-2) for a safe API.

Set `LLAMA_CPP_LIBS` to an installed prefix containing `include/`, `lib/`,
`bin/` on Windows, and `backends/` with the `dynamic-backends` feature. This
requires `dynamic-link` and bypasses CMake and GPU toolkit detection. The
installed headers must match the vendored llama.cpp headers. Bindgen still
runs; the small Rust common wrapper still compiles when `common` is enabled.
The prefix must then also contain the `llama-common` shared library and the
`llama-common-base` static archive in `lib/`. `mtmd` requires its static archive there too.

Backend modules are exposed as `DEP_LLAMA_BACKENDS_DIR`. Load them with
`llama_cpp_2::llama_backend::load_backends()` before backend initialization.
Arrange for the platform loader to find `lib/` (or `bin/` on Windows).
