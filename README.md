MTRandom
========

A Java implementation of the MT19937 (Mersenne Twister) pseudo random number generator algorithm based upon the original
C code by Makoto Matsumoto and Takuji Nishimura (see http://www.math.sci.hiroshima-u.ac.jp/~m-mat/MT/emt.html
for more information). Read the [API documentation](https://hagbard.github.io/mt-random/net/goui/util/MTRandom.html).

This class should provide a dependency free drop-in replacement for `java.util.Random` with the additional
advantage of having a far longer period, and the ability to use a far larger seed value.

This is **not** a cryptographically strong source of randomness and should **not** be
used for cryptographic systems or in any other situation where true randomness is required.

Version 1.1
-----------

Version 1.1 is an update to the original code from 2005 and changes a few small things:

1. Default seed initialization is no longer based solely on the system clock.
2. Unnecessary calls to "setSeed()" during parent class initialization are now ignored.
3. Improved JavaDoc documentation.
4. Minor code tidying.

Additionally, this version comes with unit tests and a "golden data" test to ensure stability!

NIST Randomness Tests
---------------------

The class has also been tested with the random number test suite described
at http://csrc.nist.gov/groups/ST/toolkit/random_number.html
and http://csrc.nist.gov/groups/ST/toolkit/rng/documents/SP800-22rev1a.pdf.

The test suite used is https://github.com/stamfest/randomtests, written by Peter Stamfest (but this cannot be shipped as
a dependenchy of this project for technical and licensing reasons).

The NIST test suite was run for 10 sequences of length 1,000,000 digits, and the results are:

```text
---------------------------------------------------------------------------------------------------------
RESULTS FOR THE UNIFORMITY OF P-VALUES AND THE PROPORTION OF PASSING SEQUENCES
---------------------------------------------------------------------------------------------------------
 C1  C2  C3  C4  C5  C6  C7  C8  C9 C10  P-VALUE PROPORTION STATISTICAL TEST
---------------------------------------------------------------------------------------------------------
  1   1   0   1   1   2   1   1   1   1  0.991468   10/10   Frequency
  0   1   2   2   1   0   0   2   1   1  0.739918   10/10   BlockFrequency(128)
  0   2   1   0   1   1   0   1   1   3  0.534146   10/10   CumulativeSums[forward]
  0   2   0   2   0   1   0   2   1   2  0.534146   10/10   CumulativeSums[backward]
  1   0   1   1   1   3   2   0   1   0  0.534146   10/10   Runs
  2   2   1   2   0   1   0   0   1   1  0.739918   10/10   LongestRunOfOnes
  2   1   1   1   0   1   1   1   2   0  0.911413   10/10   Rank
  1   1   1   2   1   2   0   1   0   1  0.911413   10/10   DiscreteFourierTransform
  0   1   0   2   1   1   0   1   2   2  0.739918   10/10   NonOverlappingTemplateMatchings(9)[000000001]
  1   0   1   1   0   1   1   1   1   3  0.739918   10/10   NonOverlappingTemplateMatchings(9)[000000011]
  0   2   1   4   0   0   0   1   1   1  0.122325   10/10   NonOverlappingTemplateMatchings(9)[000000101]
  0   0   4   1   1   0   3   0   0   1  0.035174   10/10   NonOverlappingTemplateMatchings(9)[000000111]
  0   3   1   0   2   0   1   2   1   0  0.350485   10/10   NonOverlappingTemplateMatchings(9)[000001001]
  3   0   1   1   0   0   1   0   4   0  0.035174    9/10   NonOverlappingTemplateMatchings(9)[000001011]
  0   2   1   0   0   2   1   2   0   2  0.534146   10/10   NonOverlappingTemplateMatchings(9)[000001101]
  1   0   0   1   1   3   0   0   2   2  0.350485   10/10   NonOverlappingTemplateMatchings(9)[000001111]
  0   0   2   5   0   0   1   1   1   0  0.008879   10/10   NonOverlappingTemplateMatchings(9)[000010001]
  0   1   0   0   1   4   2   0   1   1  0.122325   10/10   NonOverlappingTemplateMatchings(9)[000010011]
  0   1   1   0   1   1   0   2   0   4  0.122325   10/10   NonOverlappingTemplateMatchings(9)[000010101]
  0   2   1   1   0   0   2   2   1   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[000010111]
  2   0   1   1   1   1   2   1   1   0  0.911413   10/10   NonOverlappingTemplateMatchings(9)[000011001]
  0   2   1   0   1   0   1   1   1   3  0.534146   10/10   NonOverlappingTemplateMatchings(9)[000011011]
  2   0   0   0   1   1   3   0   1   2  0.350485   10/10   NonOverlappingTemplateMatchings(9)[000011101]
  2   1   3   0   0   2   1   0   0   1  0.350485   10/10   NonOverlappingTemplateMatchings(9)[000011111]
  1   0   1   1   0   2   1   2   1   1  0.911413   10/10   NonOverlappingTemplateMatchings(9)[000100011]
  0   2   1   1   2   2   0   0   1   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[000100101]
  1   2   1   1   0   1   2   0   1   1  0.911413   10/10   NonOverlappingTemplateMatchings(9)[000100111]
  1   1   1   1   1   2   0   1   0   2  0.911413   10/10   NonOverlappingTemplateMatchings(9)[000101001]
  0   1   0   1   1   2   2   1   1   1  0.911413   10/10   NonOverlappingTemplateMatchings(9)[000101011]
  0   2   0   0   1   2   1   3   1   0  0.350485   10/10   NonOverlappingTemplateMatchings(9)[000101101]
  2   0   2   1   0   1   2   0   0   2  0.534146   10/10   NonOverlappingTemplateMatchings(9)[000101111]
  1   2   1   0   2   0   0   0   1   3  0.350485   10/10   NonOverlappingTemplateMatchings(9)[000110011]
  1   3   2   0   1   1   0   0   1   1  0.534146   10/10   NonOverlappingTemplateMatchings(9)[000110101]
  0   0   2   3   0   0   0   2   2   1  0.213309   10/10   NonOverlappingTemplateMatchings(9)[000110111]
  1   0   1   2   2   2   1   1   0   0  0.739918   10/10   NonOverlappingTemplateMatchings(9)[000111001]
  0   0   1   0   4   2   1   0   1   1  0.122325   10/10   NonOverlappingTemplateMatchings(9)[000111011]
  2   1   0   0   1   3   0   0   2   1  0.350485   10/10   NonOverlappingTemplateMatchings(9)[000111101]
  1   4   0   1   3   0   0   1   0   0  0.035174   10/10   NonOverlappingTemplateMatchings(9)[000111111]
  2   1   0   0   1   1   1   1   2   1  0.911413   10/10   NonOverlappingTemplateMatchings(9)[001000011]
  1   1   1   0   2   2   1   1   1   0  0.911413   10/10   NonOverlappingTemplateMatchings(9)[001000101]
  2   2   1   0   1   0   0   2   1   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[001000111]
  3   0   1   2   2   0   0   0   0   2  0.213309   10/10   NonOverlappingTemplateMatchings(9)[001001011]
  1   1   2   0   2   1   1   1   1   0  0.911413   10/10   NonOverlappingTemplateMatchings(9)[001001101]
  3   1   0   1   2   1   0   1   0   1  0.534146    9/10   NonOverlappingTemplateMatchings(9)[001001111]
  1   3   1   1   1   1   0   0   1   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[001010011]
  3   0   2   0   0   0   0   0   3   2  0.066882   10/10   NonOverlappingTemplateMatchings(9)[001010101]
  1   3   0   1   0   1   1   1   1   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[001010111]
  2   0   2   0   0   1   1   1   1   2  0.739918   10/10   NonOverlappingTemplateMatchings(9)[001011011]
  1   0   0   1   2   0   0   5   1   0  0.008879   10/10   NonOverlappingTemplateMatchings(9)[001011101]
  3   2   1   0   1   1   0   0   1   1  0.534146   10/10   NonOverlappingTemplateMatchings(9)[001011111]
  1   0   2   2   2   0   1   2   0   0  0.534146   10/10   NonOverlappingTemplateMatchings(9)[001100101]
  1   2   2   2   1   0   0   1   0   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[001100111]
  1   0   0   1   3   3   0   0   2   0  0.122325   10/10   NonOverlappingTemplateMatchings(9)[001101011]
  0   2   3   0   1   0   0   1   1   2  0.350485   10/10   NonOverlappingTemplateMatchings(9)[001101101]
  1   0   2   1   0   2   0   1   1   2  0.739918   10/10   NonOverlappingTemplateMatchings(9)[001101111]
  1   3   2   0   0   1   0   2   1   0  0.350485   10/10   NonOverlappingTemplateMatchings(9)[001110101]
  1   1   0   1   0   2   2   2   0   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[001110111]
  0   1   1   2   1   1   2   0   1   1  0.911413   10/10   NonOverlappingTemplateMatchings(9)[001111011]
  0   4   0   2   1   1   0   1   0   1  0.122325   10/10   NonOverlappingTemplateMatchings(9)[001111101]
  2   0   0   1   2   2   0   1   1   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[001111111]
  1   2   0   1   2   1   1   0   2   0  0.739918   10/10   NonOverlappingTemplateMatchings(9)[010000011]
  1   0   0   2   3   1   3   0   0   0  0.122325   10/10   NonOverlappingTemplateMatchings(9)[010000111]
  1   1   0   0   2   3   0   0   2   1  0.350485    9/10   NonOverlappingTemplateMatchings(9)[010001011]
  0   1   0   1   1   2   3   1   0   1  0.534146   10/10   NonOverlappingTemplateMatchings(9)[010001111]
  1   2   1   1   0   1   1   0   2   1  0.911413   10/10   NonOverlappingTemplateMatchings(9)[010010011]
  1   1   0   3   1   1   0   0   1   2  0.534146    9/10   NonOverlappingTemplateMatchings(9)[010010111]
  2   0   1   0   0   1   1   4   0   1  0.122325    8/10   NonOverlappingTemplateMatchings(9)[010011011]
  1   0   0   1   0   2   2   2   1   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[010011111]
  1   1   1   0   0   2   2   1   2   0  0.739918   10/10   NonOverlappingTemplateMatchings(9)[010100011]
  1   3   0   1   0   0   2   0   1   2  0.350485   10/10   NonOverlappingTemplateMatchings(9)[010100111]
  1   4   1   1   2   0   0   1   0   0  0.122325   10/10   NonOverlappingTemplateMatchings(9)[010101011]
  2   1   1   2   1   1   1   0   1   0  0.911413   10/10   NonOverlappingTemplateMatchings(9)[010101111]
  0   1   3   2   0   2   1   0   0   1  0.350485   10/10   NonOverlappingTemplateMatchings(9)[010110011]
  0   1   0   2   3   0   0   1   3   0  0.122325   10/10   NonOverlappingTemplateMatchings(9)[010110111]
  2   1   0   1   0   1   0   0   4   1  0.122325    9/10   NonOverlappingTemplateMatchings(9)[010111011]
  1   4   1   1   0   0   1   1   0   1  0.213309   10/10   NonOverlappingTemplateMatchings(9)[010111111]
  3   1   0   0   0   1   2   0   3   0  0.122325   10/10   NonOverlappingTemplateMatchings(9)[011000111]
  1   1   1   2   1   2   1   1   0   0  0.911413    9/10   NonOverlappingTemplateMatchings(9)[011001111]
  1   1   1   0   2   2   2   0   0   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[011010111]
  1   1   1   0   0   1   1   3   0   2  0.534146   10/10   NonOverlappingTemplateMatchings(9)[011011111]
  0   0   2   2   1   2   2   0   1   0  0.534146   10/10   NonOverlappingTemplateMatchings(9)[011101111]
  1   1   0   2   1   0   0   1   0   4  0.122325   10/10   NonOverlappingTemplateMatchings(9)[011111111]
  0   1   0   2   1   1   0   1   2   2  0.739918   10/10   NonOverlappingTemplateMatchings(9)[100000000]
  2   2   0   0   0   1   3   1   0   1  0.350485   10/10   NonOverlappingTemplateMatchings(9)[100010000]
  1   0   3   0   0   4   0   1   0   1  0.035174    9/10   NonOverlappingTemplateMatchings(9)[100100000]
  2   0   0   0   1   3   1   1   1   1  0.534146   10/10   NonOverlappingTemplateMatchings(9)[100101000]
  1   1   1   0   0   3   0   1   1   2  0.534146   10/10   NonOverlappingTemplateMatchings(9)[100110000]
  3   0   0   1   1   2   2   0   1   0  0.350485   10/10   NonOverlappingTemplateMatchings(9)[100111000]
  3   0   0   2   0   1   0   2   0   2  0.213309   10/10   NonOverlappingTemplateMatchings(9)[101000000]
  2   0   2   1   1   0   1   1   1   1  0.911413   10/10   NonOverlappingTemplateMatchings(9)[101000100]
  0   0   3   3   1   0   0   2   0   1  0.122325   10/10   NonOverlappingTemplateMatchings(9)[101001000]
  0   2   1   0   0   2   1   1   2   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[101001100]
  2   0   2   0   2   2   1   1   0   0  0.534146   10/10   NonOverlappingTemplateMatchings(9)[101010000]
  0   1   1   1   0   0   0   4   1   2  0.122325   10/10   NonOverlappingTemplateMatchings(9)[101010100]
  0   2   1   0   2   0   2   0   3   0  0.213309   10/10   NonOverlappingTemplateMatchings(9)[101011000]
  1   1   1   2   0   0   1   0   1   3  0.534146   10/10   NonOverlappingTemplateMatchings(9)[101011100]
  2   1   1   2   0   2   0   0   1   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[101100000]
  1   0   1   3   1   0   1   1   0   2  0.534146   10/10   NonOverlappingTemplateMatchings(9)[101100100]
  1   4   1   0   1   1   1   0   1   0  0.213309   10/10   NonOverlappingTemplateMatchings(9)[101101000]
  2   0   0   0   1   2   2   2   0   1  0.534146   10/10   NonOverlappingTemplateMatchings(9)[101101100]
  1   0   1   0   0   1   1   3   3   0  0.213309   10/10   NonOverlappingTemplateMatchings(9)[101110000]
  3   1   0   1   0   0   1   2   1   1  0.534146   10/10   NonOverlappingTemplateMatchings(9)[101110100]
  1   1   0   1   0   0   2   2   1   2  0.739918   10/10   NonOverlappingTemplateMatchings(9)[101111000]
  1   1   1   1   1   3   0   0   0   2  0.534146   10/10   NonOverlappingTemplateMatchings(9)[101111100]
  0   0   1   0   2   0   1   2   1   3  0.350485   10/10   NonOverlappingTemplateMatchings(9)[110000000]
  1   0   0   0   1   1   1   1   4   1  0.213309   10/10   NonOverlappingTemplateMatchings(9)[110000010]
  0   0   1   1   0   5   0   2   0   1  0.008879   10/10   NonOverlappingTemplateMatchings(9)[110000100]
  1   0   1   0   3   0   2   3   0   0  0.122325   10/10   NonOverlappingTemplateMatchings(9)[110001000]
  0   2   2   1   0   2   0   2   1   0  0.534146   10/10   NonOverlappingTemplateMatchings(9)[110001010]
  1   1   1   0   1   3   0   1   1   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[110010000]
  1   1   0   1   1   1   0   1   1   3  0.739918   10/10   NonOverlappingTemplateMatchings(9)[110010010]
  1   3   1   0   0   1   1   2   1   0  0.534146   10/10   NonOverlappingTemplateMatchings(9)[110010100]
  0   1   1   1   2   4   0   0   1   0  0.122325   10/10   NonOverlappingTemplateMatchings(9)[110011000]
  3   0   0   0   1   2   2   1   0   1  0.350485    9/10   NonOverlappingTemplateMatchings(9)[110011010]
  0   2   1   0   1   2   1   1   1   1  0.911413   10/10   NonOverlappingTemplateMatchings(9)[110100000]
  4   0   1   2   0   1   2   0   0   0  0.066882    8/10   NonOverlappingTemplateMatchings(9)[110100010]
  0   1   1   2   1   1   1   2   0   1  0.911413   10/10   NonOverlappingTemplateMatchings(9)[110100100]
  2   1   0   0   1   0   3   0   2   1  0.350485    9/10   NonOverlappingTemplateMatchings(9)[110101000]
  0   0   1   1   3   2   0   1   1   1  0.534146   10/10   NonOverlappingTemplateMatchings(9)[110101010]
  0   1   0   1   4   2   1   0   1   0  0.122325   10/10   NonOverlappingTemplateMatchings(9)[110101100]
  2   0   1   2   0   1   1   1   1   1  0.911413   10/10   NonOverlappingTemplateMatchings(9)[110110000]
  2   2   1   0   0   1   0   1   1   2  0.739918    9/10   NonOverlappingTemplateMatchings(9)[110110010]
  1   0   2   0   3   1   2   0   1   0  0.350485   10/10   NonOverlappingTemplateMatchings(9)[110110100]
  1   1   1   1   0   4   0   0   0   2  0.122325   10/10   NonOverlappingTemplateMatchings(9)[110111000]
  2   0   1   0   0   2   1   1   2   1  0.739918    9/10   NonOverlappingTemplateMatchings(9)[110111010]
  0   0   2   0   1   2   0   0   1   4  0.066882   10/10   NonOverlappingTemplateMatchings(9)[110111100]
  0   3   0   2   1   0   2   0   1   1  0.350485   10/10   NonOverlappingTemplateMatchings(9)[111000000]
  0   0   2   4   0   0   1   0   2   1  0.066882   10/10   NonOverlappingTemplateMatchings(9)[111000010]
  1   1   0   0   0   2   3   1   1   1  0.534146   10/10   NonOverlappingTemplateMatchings(9)[111000100]
  1   2   0   0   1   1   0   1   2   2  0.739918   10/10   NonOverlappingTemplateMatchings(9)[111000110]
  0   0   2   2   0   3   1   1   1   0  0.350485   10/10   NonOverlappingTemplateMatchings(9)[111001000]
  2   1   2   0   1   0   1   2   1   0  0.739918   10/10   NonOverlappingTemplateMatchings(9)[111001010]
  0   2   0   2   0   0   2   1   2   1  0.534146   10/10   NonOverlappingTemplateMatchings(9)[111001100]
  3   2   1   1   1   1   0   0   1   0  0.534146   10/10   NonOverlappingTemplateMatchings(9)[111010000]
  1   1   2   1   1   0   3   0   1   0  0.534146   10/10   NonOverlappingTemplateMatchings(9)[111010010]
  1   1   1   2   0   0   2   3   0   0  0.350485   10/10   NonOverlappingTemplateMatchings(9)[111010100]
  1   2   0   1   0   2   1   0   2   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[111010110]
  2   1   1   1   2   1   0   0   0   2  0.739918   10/10   NonOverlappingTemplateMatchings(9)[111011000]
  0   1   2   0   0   2   1   2   1   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[111011010]
  3   0   2   2   1   2   0   0   0   0  0.213309    9/10   NonOverlappingTemplateMatchings(9)[111011100]
  0   1   0   3   0   3   0   1   2   0  0.122325   10/10   NonOverlappingTemplateMatchings(9)[111100000]
  0   2   0   1   0   1   0   2   0   4  0.066882   10/10   NonOverlappingTemplateMatchings(9)[111100010]
  2   1   2   1   1   0   0   1   2   0  0.739918   10/10   NonOverlappingTemplateMatchings(9)[111100100]
  1   0   3   1   1   2   1   1   0   0  0.534146   10/10   NonOverlappingTemplateMatchings(9)[111100110]
  2   0   0   2   0   1   0   1   4   0  0.066882   10/10   NonOverlappingTemplateMatchings(9)[111101000]
  1   1   0   0   1   4   0   2   0   1  0.122325   10/10   NonOverlappingTemplateMatchings(9)[111101010]
  1   1   0   2   0   1   1   2   1   1  0.911413   10/10   NonOverlappingTemplateMatchings(9)[111101100]
  0   0   3   2   0   0   2   0   2   1  0.213309   10/10   NonOverlappingTemplateMatchings(9)[111101110]
  1   1   1   1   0   3   0   1   2   0  0.534146    9/10   NonOverlappingTemplateMatchings(9)[111110000]
  4   0   1   1   1   3   0   0   0   0  0.035174   10/10   NonOverlappingTemplateMatchings(9)[111110010]
  3   0   2   1   0   0   1   2   1   0  0.350485   10/10   NonOverlappingTemplateMatchings(9)[111110100]
  0   1   0   1   1   0   1   0   3   3  0.213309   10/10   NonOverlappingTemplateMatchings(9)[111110110]
  2   2   1   1   0   2   0   0   1   1  0.739918   10/10   NonOverlappingTemplateMatchings(9)[111111000]
  3   1   3   1   1   0   0   0   0   1  0.213309   10/10   NonOverlappingTemplateMatchings(9)[111111010]
  0   2   0   0   1   1   2   1   1   2  0.739918   10/10   NonOverlappingTemplateMatchings(9)[111111100]
  1   1   0   2   1   0   0   1   0   4  0.122325   10/10   NonOverlappingTemplateMatchings(9)[111111110]
  0   5   0   0   2   1   1   0   0   1  0.008879   10/10   OverlappingTemplateMatching(9)
  0   1   0   2   1   3   1   0   1   1  0.534146   10/10   Universal
  2   0   1   0   1   1   2   0   2   1  0.739918   10/10   ApproximateEntropy(10)
  1   0   0   2   0   0   4   0   0   1    ----      8/8    RandomExcursions[-4]
  1   0   1   1   0   2   1   0   0   2    ----      8/8    RandomExcursions[-3]
  0   2   2   1   0   2   0   0   0   1    ----      8/8    RandomExcursions[-2]
  1   0   0   0   1   0   2   1   1   2    ----      8/8    RandomExcursions[-1]
  2   0   0   0   0   1   2   2   0   1    ----      8/8    RandomExcursions[1]
  3   1   0   0   0   1   2   0   1   0    ----      8/8    RandomExcursions[2]
  1   2   3   1   0   0   0   1   0   0    ----      8/8    RandomExcursions[3]
  1   2   1   0   0   0   3   0   1   0    ----      8/8    RandomExcursions[4]
  1   0   0   1   1   2   0   2   0   1    ----      8/8    RandomExcursionsVariant[-9]
  0   1   0   1   0   3   1   0   1   1    ----      8/8    RandomExcursionsVariant[-8]
  0   1   0   1   1   2   1   1   1   0    ----      8/8    RandomExcursionsVariant[-7]
  0   1   0   2   3   2   0   0   0   0    ----      8/8    RandomExcursionsVariant[-6]
  1   1   1   2   0   2   0   0   1   0    ----      8/8    RandomExcursionsVariant[-5]
  2   0   1   2   1   0   0   0   0   2    ----      8/8    RandomExcursionsVariant[-4]
  1   2   1   0   1   0   2   0   0   1    ----      8/8    RandomExcursionsVariant[-3]
  1   0   3   1   0   0   2   1   0   0    ----      8/8    RandomExcursionsVariant[-2]
  0   2   1   0   1   1   1   1   0   1    ----      8/8    RandomExcursionsVariant[-1]
  0   0   2   2   2   0   0   1   1   0    ----      8/8    RandomExcursionsVariant[1]
  0   3   1   1   1   0   0   1   1   0    ----      8/8    RandomExcursionsVariant[2]
  1   3   0   1   0   0   1   0   0   2    ----      8/8    RandomExcursionsVariant[3]
  1   1   1   1   1   0   1   1   0   1    ----      8/8    RandomExcursionsVariant[4]
  0   2   2   0   0   2   1   0   0   1    ----      8/8    RandomExcursionsVariant[5]
  1   1   0   0   0   2   3   0   0   1    ----      8/8    RandomExcursionsVariant[6]
  1   1   0   0   0   1   0   2   1   2    ----      8/8    RandomExcursionsVariant[7]
  1   1   0   0   1   0   2   2   0   1    ----      8/8    RandomExcursionsVariant[8]
  1   1   0   0   1   1   2   0   0   2    ----      8/8    RandomExcursionsVariant[9]
  0   0   2   2   3   1   2   0   0   0  0.213309   10/10   Serial(16)[1]
  1   0   3   3   0   1   1   1   0   0  0.213309   10/10   Serial(16)[2]
  0   1   1   1   1   3   0   1   0   2  0.534146   10/10   LinearComplexity(500)
```

Interpreting the results is not trivial, and the tests are (by their nature) non-repeatable, but the summary shows
that for each test all, or almost all, of the sequences tested satisfy the test criteria (e.g. `9/10` or `10/10`).

A random sequence can always exhibit apparent "structure" purely by chance, so having a small number of sequences "fail"
is not unexpected. What's important is that for all tests, over multiple runs, most sequences pass.
