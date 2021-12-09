# Random Number Generation

The existing RNG APIs defined as `base::RandBytes` and by extension,
`crypto::RandBytes` are used throughout the browser for random number
generation. They're secure enough for cryptography and can be used
interchangeably. The APIs in `base/rand_util.cc` are cleanly separated into the
secure and `InsecureRandomGenerator` classes; the latter is a xorshift128+ RNG
seeded by the secure RNG and is significantly faster than the former due its
simple construction and lack of syscall overhead. We're going to be investing in
development of a ChaCha CSPRNG to significantly speed up random number
generation — it's going to initially be used by PartitionAlloc for its
probabilistic defenses but it's likely we'll extend it to other components that
requre a secure CSPRNG.
