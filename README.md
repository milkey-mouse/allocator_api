# allocator_api

This is a copy of parts of the unstable allocator_api
(https://github.com/rust-lang/rust/issues/32838)

Usable with stable rust, but requires 1.25.

## Differences with nightly rust

The code was copied from src/liballoc as of
92bfcd2b192e59d12d64acf6f46c1897a3273b3e, with #[unstable] annotations removed.

In the allocator module, the `oom` function calls `panic!` instead of
`core::intrinsics::abort`, which is not stable. This presumes `panic!`
doesn't require memory allocation.

In the raw_vec module, `RawVec` uses `NonNull` instead of `Unique`.

The `Heap` struct, enabled by the `heap` feature of this crate, wraps the
`Heap` from liballoc, and thus requires nightly rustc. Consequently, all
functionality using `Heap` is disabled by default.
