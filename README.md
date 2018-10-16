# Schedulex

This is a scheduler for elixir that runs all jobs in a given module on a defined interval.

## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `schedulex` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:schedulex, "~> 0.1.0"}
  ]
end
```

Schedulex needs to be run as a worker, so in your application, you'd need to add something like this.

```elixir
def start(_type, _args) do
    import Supervisor.Spec

    children = [
      worker(Schedulex, []),
    ]
    opts = [strategy: :one_for_one, name: MyApp.Supervisor]
    Supervisor.start_link(children, opts)
  end

```

## Configuration

Schedulex requires two configuration keys:

```elixir
config :schedulex, interval_minutes: 5, job_module: MyApp.JobsModule
```

### Interval Minutes

This is how often the jobs module's `run` function will be called. Putting an interval of `5` would run the module on every 5 minute interval of an hour. <b>Note that this does not run every 5 minutes since the scheduler has started.</b>

### Job Module

This is a module that simply needs to have a public `run/0`.

## Further Documentation

Documentation can be generated with [ExDoc](https://github.com/elixir-lang/ex_doc)
and published on [HexDocs](https://hexdocs.pm). Once published, the docs can
be found at [https://hexdocs.pm/schedulex](https://hexdocs.pm/schedulex).