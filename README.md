# ![PackingPeanut Logo](./_art/logo_100.png) PackingPeanut [![Gem Version](https://badge.fury.io/rb/PackingPeanut.svg)](http://badge.fury.io/rb/PackingPeanut)

### Cross Platform App Persistence
![cross platform rubymotion gem](./_art/both_icon.png)

Inspired by BubbleWrap's easy syntax for App Persistence - Now a CROSS PLATFORM App Persistence Gem for RubyMotion.

There is a sedulous effort to make this syntax fit BubbleWrap's as much as possible for easy replacement :smiling_imp:

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
```ruby
# ONLY ANDROID REQUIRES CONTEXT!
# See the section on Android context for more info
$ App::Persistence.context = self
=> #<MainActivity:0x1d20058e>
$ App::Persistence['dinner'] = "nachos"
=> "nachos"
$ App::Persistence['dinner']
=> "nachos"
$ App::Persistence[:lunch] = "tacos"
=> "tacos" # Use symbols or strings as you please
$ App::Persistence.all
=> {"dinner"=>"nachos", "lunch"=>"tacos"}
$ App::Persistence.storage_file = "some_new_file"
=> "some_new_file"
$ App::Persistence['dinner']
=> nil  # empty because we're now outside the default storage file.
```

Friendly aliases:
```ruby
# You can use PP instead of App::Persistence if you like
$ PP['some_boolean'] = true
# You can use PackingPeanut (true name) if you like
$ PackingPeanut['so_easy'] = true
```

Access deeper features:
```ruby
# On Android you can set prefrence_modes for cross/app communication
$ App::Persistence.preference_mode = :world_readable
=> :world_readable
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
Adding [Darin's moran gem](https://github.com/darinwilson/moran) allowed serialization of hashes for Android.  This means `motion-gradle` is also necessary for complete Packing Peanut excellence on Android.

## Tests?

  * **iOS:** Yup!
  * **Android:** Boy that would be nice wouldn't it?

## PackingPeanut Alongside Bubblewrap on iOS?
It's meant to look just like BubbleWrap, not fight with it.   If you include the BubbleWrap library, PackingPeanut will gracefully bow out of the App::Persistence namespace.  You can still access PackingPeanut with `PP` or `PackingPeanut`.

## Explain this Android `context` _thing_ Again
Just like a conversation taken out of context can be confusing, Android has a lot of moving parts and requires just about EVERYTHING that would be a lib component to understand the context.   When accessing persistent data, context is required.   You can easily handle this by giving PackingPeanut your application context in your Application startup file.

PackingPeanut Context Examples:
```ruby
# Providing Context - Regular
class MyApplication < Android::App::Application
  def onCreate
    PP.context = self
  end
end

# Providing Context with BluePotion
class MyApplication < PMApplication
  def on_create
    PP.context = self
  end
end
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Ponder life... for at least like... 5 minutes
6. Create new Pull Request
