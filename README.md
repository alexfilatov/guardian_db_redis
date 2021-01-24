# GuardianDb Redis Repo

## Installation

1. You need to add [`:redix`](https://github.com/whatyouhide/redix) and [`:jason`](https://github.com/michalmuskala/jason) to your project to make this Redis "Repo" working for your Guardian.DB

in your `mix.exs` file:
```elixir
{:redix, ">= 0.0.0"},
{:jason, "~> 1.0"},
```
and create a config:

```elixir
config :my_app, :redis,
  host: {:system, "REDIS_HOST"},
  port: {:system, "REDIS_PORT"}
```

2. Create `MyApp.Redix` module in your `lib/` directory. This is pool of Redix workers, just to be sure you'll not face GenServer bottleneck.
   
   Apart from that, don't forget to add `MyApp.Redix` to your `application.ex` file as a child to your Supervisor so it will be started when your project starts.

```elixir
    children = [
      ...
      MyApp.Redix,
      ...
    ]
```


3. Update your `config/config.exs` file with `Guardian.DB` config:

```elixir
config :guardian, Guardian.DB,
  repo: Guardian.DB.Repo.Redis
```

You're done! Now your Guardian tokens are stored in Redis.
