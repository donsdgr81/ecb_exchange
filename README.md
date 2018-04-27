# ECB Exchange Convertor

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'ecb_exchange'
```

And then execute:

    $ bundle

## Requirements

This gem requires a working cache object that responds to read/write methods. By
default the `Rails.cache` object will be used if it is available.

Or you can configure your own cache backend store (in an initializer) like so;

    ECB::Exchange::Cache.backend =  # your cache here ...

If no backend cache store is available a `NullBackend` will be used and nothing
will be cached.

All rates stored in the cache are name-spaced with a key prefix.

## Usage

Exchange rates can be fetched like so:

    ECB::Exchange::XMLFeed.fetch

The feed will fetch and cache ECB rates for the last 90 days. You can then ask
for an exchange rate on a given day like so:

    ExchangeRate.at('2016-01-22', 'USD', 'GBP')

If the cache is empty rates will be fetched from the endpoint and the cache will
be populated. You can adjust which endpoint rates are fetched from in an
initializer like so;

    ECB::Exchange::XMLFeed.endpoint = "http://my-awesome-service.com/feed.xml"

The XML feed must match the standard [ECB
rates](http://www.ecb.europa.eu/stats/eurofxref/eurofxref-hist-90d.xml) structure.

## Errors

Not all dates and rates may be available, or the feed server may be down. You
should consider how to handle the following errors.

* `ECB::Exchange::DateNotFoundError`
* `ECB::Exchange::CurrencyNotFoundError`
* `ECB::Exchange::ResponseError`
* `ECB::Exchange::ParseError`

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake test` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

