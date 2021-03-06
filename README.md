ioredis-mock
============

[![AppVeyor branch](https://img.shields.io/appveyor/ci/stipsan/ioredis-mock/master.svg?label=windows)](https://ci.appveyor.com/project/stipsan/ioredis-mock)
[![Travis branch](https://img.shields.io/travis/stipsan/ioredis-mock/master.svg?label=linux)](https://travis-ci.org/stipsan/ioredis-mock)
[![CircleCI](https://img.shields.io/circleci/project/stipsan/ioredis-mock/master.svg?label=node+matrix)](https://circleci.com/gh/stipsan/ioredis-mock)
[![Code Climate](https://codeclimate.com/github/stipsan/ioredis-mock/badges/gpa.svg)](https://codeclimate.com/github/stipsan/ioredis-mock)
[![Coverage Status](https://coveralls.io/repos/github/stipsan/ioredis-mock/badge.svg)](https://coveralls.io/github/stipsan/ioredis-mock)
[![Redis Compatibility: 49%](https://img.shields.io/badge/redis-49%25-yellow.svg)](compat.md)
[![npm package](https://img.shields.io/npm/dm/ioredis-mock.svg)](https://www.npmjs.com/package/ioredis-mock)

[![NPM](https://nodei.co/npm/ioredis-mock.png?downloadRank=true)](https://www.npmjs.com/package/ioredis-mock)
[![NPM](https://nodei.co/npm-dl/ioredis-mock.png?months=3&height=2)](https://nodei.co/npm/ioredis-mock/)

This library emulates [ioredis](https://github.com/luin/ioredis) by performing all operations in-memory.
The best way to do integration testing against redis and ioredis is on a real redis-server instance.
However, there are cases where mocking the redis-server is a better option.

Cases like:

* Your workflow already use a local redis-server instance for the dev server.
* You're on a platform [without an official redis release](https://github.com/MSOpenTech/redis), that's even worse than using an emulator.
* You're running tests on a CI, setting it up is complicated. If you combine it with CI that also run selenium acceptance testing it's even more complicated, as two redis-server instances on the same CI build is hard.
* The GitHub repo have bots that run the testing suite and is limited through npm package.json install scripts and can't fire up servers. (Having [Greenkeeper](https://greenkeeper.io/) notifying you when a new release of ioredis is out and wether your code breaks or not is awesome).

Check the [compatibility table](compat.md) for supported redis commands.

## Usage ([try it in your browser](https://runkit.com/npm/ioredis-mock))

```js
var RedisMock = require('ioredis-mock').default;
var redis = new RedisMock({
  data: {
    user_next: '3',
    emails: {
      'clark@daily.planet': '1',
      'bruce@wayne.enterprises': '2',
    },
    'user:1': { id: '1', username: 'superman', email: 'clark@daily.planet' },
    'user:2': { id: '2', username: 'batman', email: 'bruce@wayne.enterprises' },
  }
});
// Basically use it just like ioredis
```

## Roadmap
This project started off as just an utility in [another project](https://github.com/stipsan/epic) and just recently got open sourced to benefit the rest of the ioredis community. This means there's work to do before it's feature complete:
- [x] Setup testing suite for the library itself.
- [x] Refactor to bluebird promises like ioredis, support node style callback too.
- [ ] Implement remaining basic features that read/write data.
- [ ] Implement ioredis [argument and reply transformers](https://github.com/luin/ioredis#transforming-arguments--replies).
- [ ] Connection Events
- [ ] Offline Queue
- [ ] Pub/Sub
- [ ] Error Handling

## I need a feature not listed here

Just create an issue and tell us all about it or submit a PR with it! :-)
