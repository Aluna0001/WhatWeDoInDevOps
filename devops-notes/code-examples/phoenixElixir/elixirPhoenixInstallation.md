# Elixir Installation og Syntax Noter

## Installation Process

### Hvad der skete under installationen:

1. **Erlang** blev installeret først (132 MB) - det underliggende system som Elixir kører på
2. **Elixir** blev derefter installeret (7.57 MB) - selve programmeringssproget
3. Begge blev placeret i de rigtige mapper og tilføjet til systemets PATH

### Tilgængelige kommandoer efter installation:

* `elixir` - kører Elixir scripts
* `mix` - Elixirs build-værktøj (bruges til Phoenix)
* `iex` - interaktiv Elixir shell

## Miljøvariabler og PATH

### Kort forklaring af PATH:
**PATH** er en speciel miljøvariabel som fortæller Windows hvor den skal lede efter programmer, når du skriver kommandoer i terminalen.

### Troubleshooting PATH problem:
* Chocolatey installerede Elixir i `C:\ProgramData\chocolatey\lib\Elixir\tools\bin`
* Men glemte at tilføje denne mappe til PATH-variabel
* Windows vidste ikke hvor `elixir.exe` lå
* Løsning: `$env:PATH += ";C:\ProgramData\chocolatey\lib\Elixir\tools\bin"`
* **OBS:** Miljøvariabler i PowerShell forsvinder når du lukker terminalen

## Phoenix Framework

### Installation:
Næste skridt: Installer Phoenix framework

### Dependencies i Elixir/Phoenix:
Findes i `mix.exs` filen (ligesom `pom.xml` i Maven). Typiske dependencies:
* `phoenix` - web framework
* `ecto` - database layer
* `postgrex` - PostgreSQL driver
* `jason` - JSON parser
* `plug_cowboy` - web server

## Configuration Files

### Gitignore regler:
* **IDE config** (`.idea`, `.vscode`) = personlig, skal i `.gitignore`
* **App config** (`config/dev.exs`) = deles med teamet, skal IKKE i `.gitignore`

## Database

### PostgreSQL og psql:
* **psql** er kun en terminal-klient til PostgreSQL (ingen GUI som MySQL Workbench)
* I Elixir bruger man typisk **Ecto** (ORM) + en **Repo** til at tale med PostgreSQL
* PostgreSQL selv leverer kun en CLI-klient (psql)

## Phoenix Router

**DEFAULT ER ROUTEREN. DEN ER ADSKILT.**

Routeren adskiller API og ruter som standard. Hvis vi skal have flere ruter eller API'er så kan vi tilføje dem der.

## Elixir Syntax

### Pattern Matching
```elixir
# PATTERN MATCHING (findes ikke i Java!)
# Match direkte på værdier
def describe_number(0), do: "zero"
def describe_number(1), do: "one" 
def describe_number(n), do: "number #{n}"
```

Pattern matching på argumenter i stedet for if-statements:
```elixir
def connect_db(:init), do: :sqlite3.open(@database_path)
def connect_db(:normal) do
  check_db_exists()
  :sqlite3.open(@database_path)
end
```

### Vigtige forskelle fra Java:
* Ingen `return` keyword - sidste udtryk returneres automatisk
* Ingen klasser - funktioner står selv
* `do...end` blokke eller kort `,do:` syntax
* Guards (`when`) til validering

### Kort syntax:
```elixir
def add(a, b), do: a + b  # Ingen end nødvendig
if condition, do: "yes", else: "no"
```

### Error Handling (Elixir-style):
```elixir
def connect_db(mode \\ :normal) do
  case mode do
    :init ->
      :sqlite3.open(@database_path)
    :normal ->
      with :ok <- check_db_exists() do
        :sqlite3.open(@database_path)
      else
        {:error, reason} -> {:error, "Database check failed: #{reason}"}
      end
  end
end
```

## Pipelines

[Afsnit om pipelines - tekst ikke fuldført i originale noter]