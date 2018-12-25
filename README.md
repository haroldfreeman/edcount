edcount
-------

[![Build Status](https://travis-ci.com/haroldfreeman/edcount.svg?branch=master)](https://travis-ci.com/haroldfreeman/edcount)

<p align="center">
    <img src="https://raw.githubusercontent.com/haroldfreeman/edcount/master/demo/edcount_demo.svg">
</p>

Estimate distinct count of values from standard input. Provides a very fast
way to perform unique count estimates on the command line.

A value is considered terminated with a newline.

Why use it?
-----------

If you want to quickly process a large number of values and find out roughly
how many of them are unique.

The program is well suited to estimating unique counts of billions of unique
values.

How it works
------------

The edcount program implements HyperLogLog, with some minor modifications,
as detailed by by Flajolet et. al. in the paper "HyperLogLog: the analysis of
a near-optimal cardinality estimation algorithm".

Additionally, the memory footprint of the program is constant, at a few
megabytes. This memory use is constant regardless of the number of records
counted, and does not degrade in accuracy.

Benchmark
---------

Counting 10 million unique records with sort and wc:

```
$ seq 1 10000000 | shuf | sort -u | wc -l
10000000
real  1m16.213s
user  1m13.516s
sys   0m1.516s
```

Counting 10 million unique records with edcount:

```
$ seq 1 10000000 | shuf | edcount
9988659
real  0m1.110s
user  0m1.172s
sys   0m0.180s
```

This is a 0.11% difference from the actual unique value.

Fast Install Instructions
-------------------------

Required software: `make`,`gcc`

```
curl -L -o edcount-1.2.0.tar.gz https://github.com/haroldfreeman/edcount/releases/download/v1.2.0/edcount-1.2.0.tar.gz
tar -xzvf edcount-1.2.0.tar.gz
cd edcount-1.2.0
./configure
make
make install
```

You might have to use `sudo make install` instead of `make install`.

For more detail, see the INSTALL file.

Contributing / Development
--------------------------

See the CONTRIBUTING file.

License
-------

GPLv3+, see the COPYING file.
