# SilverStripe JSONText

[![Build Status](https://api.travis-ci.org/phptek/silverstripe-jsontext.svg?branch=master)](https://travis-ci.org/phptek/silverstripe-jsontext)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/phptek/silverstripe-jsontext/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/phptek/silverstripe-jsontext/?branch=master)
[![License](https://poser.pugx.org/phptek/jsontext/license.svg)](https://github.com/phptek/silverstripe-jsontext/blob/master/LICENSE.md)

JSON storage and querying.

## Requirements

* PHP 5.4+
* SilverStripe Framework 3.1+
* SilverStripe CMS 3.1+

## Introduction

The module exposes a fully featured JSON query and update API allowing developers to use either XPath-like queries using [JSONPath](http://goessner.net/articles/JsonPath/)
or a JSON-aware RDBMS-like syntax such as those found in the [JSON operators of Postgres v9.2+](https://www.postgresql.org/docs/9.5/static/functions-json.html),
- but with some modifications - to query and update JSON data.

In Postgres both the `->` and `->>` operators act as string and integer key matchers on a JSON array or object respectively. The module
however treats both source types the same - they are after all *both JSON* so `->` is used as an **Integer Matcher** and `->>` as a **String Matcher**
*regardless* of the "type" of source JSON stored.

In Postgress the `#>` path match operator can act as an object or a text matcher, but the module wishes to simplify things and as such
the `#>` operator is *just a simple path matcher*.

I see nothing but confusion arising if the same operator were to be treated differently
depending on the specific *type of JSON* stored. I'm a reasonable man however, and am prepared for a discussion :-)

Regardless of the type of query in-use you can set what form you'd like the data returned in via the `setReturnType()` method, on a query by query basis. 

Legitimate types are:

* JSON
* Array
* SilverStripe

If using `SilverStripe`, the module will automatically cast the result(s) to one of SilverStripe's four native "scalar" `DBObject` subtypes:

* `Boolean`
* `Int`
* `Float`
* `Varchar`

If there are multiple results, the output will be an indexed array containing a single-value array for each result found.

See [the usage docs](docs/en/usage.md) for examples of JSONPath and Postgres queries.

Note: This module's query API is based on a relatively simple JSON to array conversion principle. 
It does *not* use Postgres' or MySQL's JSON operators at the ORM level. The aim however 
is to allow dev's to use their preferred DB's syntax, and to this end you can set
the module into `mysql` or `postgres` mode using SS config, see [Configuration Docs](docs/en/configuration.md).

## Installation

    #> composer require phptek/jsontext dev-master

## Configuration

See: [Configuration Docs](docs/en/configuration.md).

## Usage

See: [Usage Docs](docs/en/usage.md). 

## Stability

This is currently *alpha software*. At time of writing (June 2016) there is
support for the `->` (Int matcher), `->>` (String matcher) and `#>` (Path matcher) operators and although well-tested, 
they are far from complete.

This leads me to..

## Contributing

If you've been using Postgres or MySQL with its JSON functions for some time,
I'm keen to hear from you. Some simple failing tests would be most welcome.

See: [CONTRIBUTING.md](CONTRIBUTING.md).

## Reporting an issue

Please include all details, no matter how small. If it were *your module*, what would you need to know from a bug/feature request? :-)

## Credits

* [Axel Anceau](https://github.com/Peekmo/) for his packaging-up of the pretty amazing JSONPath implementation by [Stefan Goessner](https://code.google.com/archive/p/jsonpath/)
* [Stefan Goessner](https://code.google.com/archive/p/jsonpath/) for the original work on JSONPath dating back to 2005! 

## TODO

* Lose the fugly way that data is queried via `$this->dbObject()`

## Author

Russell Michell 2016 <russ@theruss.com>
