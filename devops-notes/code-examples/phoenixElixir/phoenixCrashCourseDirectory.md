# Phoenix Projekt Struktur

## Build og Genererede Filer

### _build
* **Dark folder (build)** - du tracker IKKE denne mappe på git
* Indeholder kompilerede filer og dependencies
* Skal tilføjes til `.gitignore`

### .elixir_ls
* **Automatic generated** - automatisk genereret af Language Server
* Editor support filer (IntelliSense, syntax highlighting)
* Skal også i `.gitignore`

## Frontend og Assets

### Assets folder
* **First important one** - hvor du gemmer alle frontend filer
* **Using Tailwind by default** - Phoenix kommer med Tailwind CSS
* Indeholder JavaScript, CSS og andre frontend ressourcer
* Tailwind kommer standard med Phoenix projekter

### Static Images
* **Static images stores on priv** - statiske billeder gemmes i priv mappen

## Konfiguration

### Config
* Indeholder alle konfigurationsfiler for forskellige miljøer
* `config.exs`, `dev.exs`, `prod.exs`, `test.exs`

## Source Code

### Lib
* **This is the source code** - her ligger din hovedkode
* Indeholder både applikationslogik og web-relateret kode

### Phoenix Contexts
I Phoenix organiserer du din business logic i "contexts":

**Når vi skal bygge features, laver vi context:**
```bash
mix phx.gen.context Shop Product products name:string price:decimal
```

* Contexts grupperer relateret funktionalitet sammen
* Gør koden mere organiseret og testbar
* Følger Domain-Driven Design principper

## Production Filer

### Priv
* **You need it in production, but it is not really part of your source code**
* Indeholder database migrations, static assets til production
* Templates, oversættelser og andre ressourcer

### Static folder
* Kompilerede og optimerede frontend assets til production
* Genereres automatisk fra assets mappen

## Dependency Management

### Mix.lock
* **Stay away from this** - rør ikke denne fil manuelt
* Låser specifikke versioner af dependencies
* Sikrer reproducible builds
* Commit til git, men rediger aldrig manuelt

## Database

### Database Filer
* **Vi kommer til at se database filerne uden for mapperne**
* SQLite database filer placeres typisk i rod-mappen under udvikling
* I production bruges ofte eksterne databaser som PostgreSQL

## Gitignore Anbefalinger

Vigtige filer at ekskludere fra git:
* `_build/`
* `.elixir_ls/`
* `deps/`
* `*.db` (SQLite database filer)
* `.env` (miljøvariabler)