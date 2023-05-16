# Friends

Following along with the [Ecto Getting Started guide](https://hexdocs.pm/ecto/getting-started.html).

## Setup

```
mix deps.get
mix ecto.create
mix ecto.migrate
```

## Cheatsheet

```elixir
# insert a record
person = %Friends.Person{}
changeset = Friends.Repo.changeset(person, %{first_name: "Alan", last_name: "Gardner"})
Friends.Repo.insert(person)
```
