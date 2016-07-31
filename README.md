# Random.Pcg for Elm

> "The generation of random numbers is too important to be left to chance." Robert R. Coveyou

An alternate random number generator. You can `import Random.Pcg as Random` and everything will continue to
work (except [elm-random-extra](http://package.elm-lang.org/packages/NoRedInk/elm-random-extra/latest/Random-Extra)).
This library offers two main improvements over core, without a large loss of performance (see `test/benchmark`):

* **Better statistical properties.** If you use any seed less than 53668 and generate one bool, it will be `True` – if
you're using the core library. This library produces far less predictable output, especially if you use thousands of
random numbers. The core library fails after as little as five seconds of scrutiny. See `test/dieharder` for more
details.

* **More features.** This library exports `constant` and `andMap`, which are conspicuously absent from core, along with
other helpful functions for composing generators. Especially interesting is the `independentSeed` function which allows
for lazy lists and isolated components to generate as much randomness as they need, when they need it. There is also a
`fastForward` function that allows random access (rather than sequential access) into, effectively, an infinite array of
random numbers. This can be used instead of reading a finite amount of random values into a large data structure.

This is an implementation of [PCG](http://www.pcg-random.org/) by M. E. O'Neil, based on the [JS
port](https://github.com/thomcc/pcg-random) by Thom Chiovoloni (MIT license). The generator is **not cryptographically
secure**.

Please report bugs, feature requests, and other issues [on GitHub](https://github.com/mgold/elm-random-pcg/issues/new).

## Changelog (major versions only)
### 3.0.0
* Change implementation to use the RXS-M-SH variant of PCG. Now much faster and not much worse statistically.
* Remove `initialSeed2`, since there are now only 32 bits of state.
* `Random.Pcg.Interop.fission` has been changed to a (core) generator of (PCG) seeds.
* Add `generate` to match core 4.x API.

### 2.0.0
* Upgraded for 0.17.
* `generate` renamed `step` to match core 4.x API.
* Module renamed `Random.Pcg` from `Random.PCG`.
* `split` has been removed; use `independentSeed`.
* `minInt` and `maxInt` values changed to match core.
