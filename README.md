Yet another Bloom filter implementation for node.js. Everybody has to write one, as you know. Backed by [Xxhash](https://code.google.com/p/xxhash/) via [node-xxhash](https://github.com/pierrec/js-xxhash). Xxhash is a fast general-purpose hash, which is all a bloom filter needs.

To install: `npm install xxbloom`

[![on npm](https://img.shields.io/npm/v/xxbloom.svg?style=flat)](https://www.npmjs.com/package/xxbloom) [![Build Status](http://img.shields.io/travis/ceejbot/xx-bloom/master.svg?style=flat)](https://travis-ci.org/ceejbot/xxbloom) [![Coverage Status](https://img.shields.io/coveralls/ceejbot/xx-bloom.svg?style=flat)](https://coveralls.io/github/ceejbot/xxbloom?branch=master)

## Usage

### BloomFilter

To create a filter, pass an options hash to the constructor:

```javascript
var options =
{
	bits: 1024,
	hashes: 7,
	seeds: [1, 2, 3, 4, 5, 6, 7]
};
filter = new BloomFilter(options);
```

You can pass in seeds for the hash functions if you like, or they'll be randomly generated. Seeds must be integers.

You may also pass in a buffer as generated by `filter.toBuffer()`.

### createOptimal()

To create a filter optimized for the number of items you'll be storing and a desired error rate:

`filter = BloomFilter.createOptimal(estimatedItemCount, errorRate);`

The error rate parameter is optional. It defaults to 0.005, or a 0.5% rate.

### add()

`filter.add('cat');`

Adds the given item to the filter. Can also accept buffers and arrays containing strings or buffers:

`filter.add(['cat', 'dog', 'coati', 'red panda']);`

### has()

To test for membership:

`filter.has('dog');`

### clear()

To clear the filter:

`filter.clear();`

### toBuffer()

Returns a buffer with seeds and filter data.

### fromBuffer()

Reconstitutes a filter from a freeze-dried buffer.

## Licence

ISC.
