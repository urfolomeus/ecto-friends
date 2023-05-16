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

# Fetching a single record
Friends.Person |> Ecto.Query.first |> Friends.Repo.one
Friends.Person |> Ecto.Query.last |> Friends.Repo.one

# Fetching a single record by ID
Friends.Person |> Friends.Repo.get(1)

# Fetching a single record by a given field
Friends.Person |> Friends.Repo.get_by(first_name: "Ryan")

# Fetching multiple records
Friends.Person |> Friends.Repo.all

# Filtering results
Friends.Person |> Ecto.Query.where(last_name: "Smith") |> Friends.Repo.all
# or...
Ecto.Query.from(p in Friends.Person, where: p.last_name == "Smith") |> Friends.Repo.all

# When using variables they must be pinned
# This triggers the use of pararmeterized SQL queries to protect against SQL Injection attacks
last_name = "Smith"
Friends.Person |> Ecto.Query.where(last_name: ^last_name) |> Friends.Repo.all
Ecto.Query.from(p in Friends.Person, where: p.last_name == ^last_name) |> Friends.Repo.all

# Composing queries
query = Friends.Person |> Ecto.Query.where(last_name: "Smith")
query = query |> Ecto.Query.where(first_name: "Jane")
query |> Friends.Repo.all

# Updating a record
person = Friends.Person |> Ecto.Query.first |> Friends.Repo.one
changeset = Friends.Person.changeset(person, %{age: 29})
Friends.Repo.update(changeset)

# Deleting a record
person = Friends.Repo.get(Friends.Person, 1)
Friends.Repo.delete(person)
```
