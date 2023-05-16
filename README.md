# Friends

Following along with the [Ecto Getting Started guide](https://hexdocs.pm/ecto/getting-started.html).

## Setup

```
mix deps.get
mix ecto.create
mix ecto.migrate
```

## Rebuild

```
mix ecto.drop
mix ecto.create
mix ecto.migrate
```

## Cheatsheet

```elixir
# insert a record
person = %Friends.Person{}
changeset = Friends.Repo.changeset(person, %{first_name: "Alan", last_name: "Gardner"})
Friends.Repo.insert(person)

# insert multiple records
people = [
  %Friends.Person{first_name: "Ryan", last_name: "Bigg", age: 28},
  %Friends.Person{first_name: "John", last_name: "Smith", age: 27},
  %Friends.Person{first_name: "Jane", last_name: "Smith", age: 26},
]
Enum.each(people, fn (person) -> Friends.Repo.insert(person) end)
```
