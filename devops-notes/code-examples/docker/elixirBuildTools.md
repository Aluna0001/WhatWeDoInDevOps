# Elixir Build Tools og Docker Deployment

## Build og Packaging Tools

* **Build tools** → mix (bygger, kompilerer, tester, håndterer dependencies)
* **Packaging** → mix release (pakker appen til en kørbar release, inkl. Erlang VM)
* **Virtualization / Containerization** → Docker eller Podman til at isolere Elixir appen
* **Docker** → container platform; typisk laver man et image med Elixir, Erlang og din app
* **Dockerfile** → skriver hvordan image bygges: installér Erlang, Elixir, hent dependencies, compile, lav release
* **Python build tools** → svarer til mix og Hex (Elixir's package manager)

## Production Environment

### Prod (Production Build)

Det betyder at Elixir bygger og optimerer appen til **produktion**:
* Ingen debug-information
* Kompileret kode er optimeret
* Konfigurationer fra `config/prod.exs` bruges (fx database, port osv.)

### Environment Sammenligning

* **dev** = udviklingsmiljø, med live reload, debugging osv.
* **test** = testmiljø, bruges under automatiserede tests
* **prod** = klar til deployment i produktion, ikke dev

## Docker Containerization

### Scaling Options
Docker: Scale vertical or horizontal (microservices)

### Step 1: Dockerfile
Contains instructions:

* **FROM** - base image
* **WORKDIR** - arbejdsmappe
* **RUN** - kommandoer der skal køres
* **COPY** - kopiér filer
* **ENV** - miljøvariabler
* **EXPOSE** - åbn porte
* **CMD** - standard kommando
* **ENTRYPOINT** - entry point
* **VOLUME** - persistente data

### Step 2: Build Image
Contains OS or dependencies. Need to run them in a container

### Docker Commands
* **Docker build -t** - bygger image med tag
* **SHA256** - image hash identifier

## Docker Compose

### Multi-container Applications
* Multiple applications and images in a simple `.yml` file
* Orchestrates multiple containers together
* Defines services, networks, and volumes

### Dockerfile Example Structure
```dockerfile
# 1. Base image med Elixir og Erlang
FROM elixir:1.15.2-alpine

# 2. Set working directory  
WORKDIR /app

# 3. Copy mix files og hent dependencies
COPY mix.exs mix.lock ./
RUN mix deps.get --only prod

# 4. Copy resten af koden og compile
COPY . .
RUN mix compile

# 5. Build release
RUN mix release

# 6. Expose port og start app
EXPOSE 4000
CMD ["_build/prod/rel/my_app/bin/my_app", "start"]
```