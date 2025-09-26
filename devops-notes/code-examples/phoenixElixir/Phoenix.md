# Phoenix Framework

## Hvad er Phoenix?

Phoenix er et web framework til Elixir - tænk Ruby on Rails eller Spring Boot til Java. Det giver dig:

* Routing (hvilke URLs der gør hvad)
* Controllers (håndterer requests)
* Views og Templates (HTML generation)
* Database integration (via Ecto)
* Real-time features (WebSockets)

## Phoenix Projekt Struktur

```
hello_world/
├── lib/
│   ├── hello_world/          # Din applikationslogik
│   └── hello_world_web/      # Web-relateret kode
│       ├── controllers/      # Håndterer HTTP requests
│       ├── views/           # Formaterer data til templates
│       ├── templates/       # HTML templates
│       └── router.ex        # URL routing
├── assets/                  # CSS, JavaScript
├── config/                  # Konfiguration
└── mix.exs                 # Projekt dependencies
```

## MVC Pattern i Phoenix

Phoenix følger Model-View-Controller pattern:

**Router** → **Controller** → **View** → **Template**

1. **Router**: Matcher URL til controller action
2. **Controller**: Håndterer request, henter data
3. **View**: Forbereder data til template
4. **Template**: Genererer HTML

## Eksempel: Tilføj en ny side

### 1. Tilføj route i router.ex:

```elixir
# lib/hello_world_web/router.ex
scope "/", HelloWorldWeb do
  pipe_through :browser
  
  get "/", PageController, :index
  get "/hello", PageController, :hello  # <-- Tilføj denne linje
end
```

### 2. Tilføj action i controller:

```elixir
# lib/hello_world_web/controllers/page_controller.ex
defmodule HelloWorldWeb.PageController do
  use HelloWorldWeb, :controller

  def index(conn, _params) do
    render(conn, "index.html")
  end

  # Tilføj denne funktion:
  def hello(conn, _params) do
    render(conn, "hello.html", name: "Verden")
  end
end
```

## Hvorfor Phoenix?

* **Performance**: Kan håndtere millioner af connections
* **Real-time**: Built-in WebSocket support
* **Productivity**: Conventions over configuration
* **Fault tolerance**: Arver Erlang/Elixir's robusthed