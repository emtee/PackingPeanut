# ![PackingPeanut Logo](./_art/logo_100.png) PackingPeanut [![Gem Version](https://badge.fury.io/rb/PackingPeanut.svg)](http://badge.fury.io/rb/PackingPeanut)

iOS has [BubbleWrap](https://github.com/rubymotion/BubbleWrap) for App Persistence : Android has PackingPeanut!

There is a sedulous effort to make this syntax fit BubbleWrap's as much as possible, but differences simply exist, either for good, technical, or sometimes diabolical reasons :smiling_imp:

[**GITHUB HOMEPAGE**](http://gantman.github.io/PackingPeanut/)

## Installation

**Step 1:** Add this line to your application's Gemfile:

    gem 'PackingPeanut'

**Step 2:** And then execute:

    $ bundle

**Step 3:** IF on Android:

    $ [bundle exec] rake gradle:install

## Usage

**It's as simple as:**
```ruby
App::Persistence[:foo] = true
# App::Persistence[:foo] would now return true
```

Whirlwind Tour via the REPL
```
# ONLY ANDROID REQUIRES CONTEXT!
# Set the context (required in the REPL or when not including the module).
$ App::Persistence.context = self
=> #<MainActivity:0x1d20058e>
$ App::Persistence['dinner'] = "nachos"
=> "nachos"
$ App::Persistence['dinner']
=> "nachos"
$ App::Persistence[:lunch] = "tacos"
=> "tacos" # Use symbols or strings as you please
$ App::Persistence.all
=> [{:dinner=>"nachos"}, {:lunch=>"tacos"}]
$ App::Persistence.storage_file = "some_new_file"
=> "some_new_file"
$ App::Persistence['dinner']
=> ""  # empty because we're now outside the default storage file.
$ App::Persistence.preference_mode = :world_readable
=> :world_readable
# You can use PP instead of App::Persistence if you like
$ PP['some_boolean'] = true
```



## What are preference modes?

Preference Modes are Android Operating modes, used to control permission levels on the persistence file.

Memorizable symbols and their corresponding constants:
```ruby
    PREFERENCE_MODES = {
      private: MODE_PRIVATE,
      readable: MODE_WORLD_READABLE,
      world_readable: MODE_WORLD_READABLE,
      writable: MODE_WORLD_WRITEABLE,
      world_writable: MODE_WORLD_WRITEABLE,
      multi: MODE_MULTI_PROCESS,
      multi_process: MODE_MULTI_PROCESS
    }
```

Use 0 or MODE_PRIVATE for the default operation, MODE_WORLD_READABLE and MODE_WORLD_WRITEABLE for more permissive modes. The bit MODE_MULTI_PROCESS can also be used if multiple processes are mutating the same SharedPreferences file. MODE_MULTI_PROCESS is always on in apps targeting Gingerbread (Android 2.3) and below, and off by default in later versions.

## Dependencies
As of version `0.0.3` there were no dependencies, but PP was completely unable to store hashes!  This was possibly due to a bug in RM Android... or a limitation of Android's JSON.  Adding [Darin's moran gem](https://github.com/darinwilson/moran) allowed serialization of hashes.  This means `motion-gradle` is also necessary for complete Packing Peanut excellence.

## Tests?
Boy that would be nice wouldn't it?

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Ponder life... for at least like... 5 minutes
6. Create new Pull Request
