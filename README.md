# RuleInterface

A ruby interface to communicate with Drools

[![Build Status](https://travis-ci.org/NestAway/rule-interface.svg?branch=master)](https://travis-ci.org/NestAway/rule-interface)

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'rule-interface'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install rule-interface

## Configuration

ENV variable can be used to configure KIE server details

`KIE_SERVER_USERNAME`, `KIE_SERVER_PASSWORD`, `KIE_SERVER_HOSTNAME`

You can also configure the KIE server details programmatically

```ruby
RuleInterface::Configuration::kiesever_config = {
  username: 'blah',
  password: 'blah',
  hostname: 'http://url',
}
```

All the attribute specified in the above configuration is optional. If specified, it will overwrite ENV configuration for that attribute

## Usage

```ruby
RuleInterface.execute!(
  data_hash: {
    product: [
      {
        id: 12,
        name: 'Blah'
      },
      {
        id: 13,
        name: 'Bla2'
      }
    ],
    user: [
      {
        id: 123,
        email: 'yoman@manyo.com'
      }
    ]
  },
  container: 'team_magic_v1.2.3',
  package: 'com.myteam.test',
  namespace: :test,
  session: 'blah'
)

You have to create data object on drools workbench first. For above example 'product' and 'user' object with respective fields id, name and email should be there.

container name also you will get from drools workbench under deployment section.For each deployment container name will be updated.

```ruby
import com.myteam.test.Product;
import com.myteam.test.User;

rule "test example" 
salience 300
no-loop true

when
  Namespace(type == 'test')
  $p: product(id == '123');
then
  System.out.println("successfully tested");
end
```

namespace is used to execute set of rules only. This is optional field. You have to create a namespace data object with a field 'type' on drools.

you have to specify your package name which you will get from drools.

session is name of your stateless session. Either you create session with default name 'session'(don't need to pass session argument) or pass it to session with you custom session name.

```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/rule-interface. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

