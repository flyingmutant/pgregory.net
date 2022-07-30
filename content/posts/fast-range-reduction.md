+++
title = "Fast range reduction with low bias"
date = 2022-07-22T23:31:24+03:00
draft = true
+++

# Fast range reduction with low bias

Say, you have a uniform 64-bit number -- usually an output of a hash
function or a random number generator -- and you want to transform it into a number
in range \[0, N), for some 32-bit N. Here is probably the best way to do it:

```c
uint32_t reduce_32x64(uint64_t x, uint32_t N) {
    return ((__uint128_t)x * (__uint128_t)N) >> 64;
}
```

This is a 32-bit adaptation of the scheme used in Stephen Canon's
["Optimal algorithm for bounded random integers"](https://github.com/apple/swift/pull/39143).
It is really fast (a single multiply instruction on a modern 64-bit processor),
but what is even better is that it gives an unbiased result with a 1 − 2⁻³²
probability. Detecting this amount of bias requires at least 2⁶⁴ results,
which is prohibitively expensive for most practical purposes. `reduce_32x64`
also works for N larger than 32 bits, but the closer you get to 64 bits, the
stronger the bias becomes.

Daniel Lemire has recently [popularized](https://lemire.me/blog/2016/06/27/a-fast-alternative-to-the-modulo-reduction/)
a similar but different algorithm:

```c
uint32_t reduce(uint32_t x, uint32_t N) {
  return ((uint64_t)x * (uint64_t)N) >> 32 ;
}
```

`reduce` is biased (similar to `x % N`). Lemire has proposed a ["nearly divisionless"](https://lemire.me/blog/2019/06/06/nearly-divisionless-random-integer-generation-on-various-systems/)
way to eliminate the bias completely, using rejection sampling. However, I believe that
between using `reduce` on a 64-bit value (throwing top 32 bits away before the multiplication)
and using a rejection sampling to eliminate bias completely, `reduce_32x64` represents
a better practical speed/quality trade-off.

Here is a [benchmark](https://github.com/flyingmutant/rand/blob/master/misc/cppbench/bench.cpp)
of a random number generation in range (using the `sfc64` generator):

| relative | ns/op | algorithm                                 |
|---------:|------:|:------------------------------------------|
|   100.0% |  3.65 | raw 64-bit random value                   |
|    59.6% |  6.13 | modulo (biased)                           |
|    88.3% |  4.14 | 32x32 fixed point (biased)                |
|    91.2% |  4.01 | 32x64 fixed point (low bias)              |
|    17.8% | 20.53 | Lemire's "Nearly Divisionless" (unbiased) |

# TODO

- grep for lemire.me/blog in OSS
  - https://docs.rs/fastrand/latest/src/fastrand/lib.rs.html#144
- link to https://github.com/lemire/fastrange/blob/master/fastrange.h
