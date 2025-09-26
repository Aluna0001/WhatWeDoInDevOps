# Phoenix Performance og Routing

## Performance og Arkitektur

### Performance Mode
* **Under the hood using Erlang** - bygget på Erlang VM
* **Using functional programming** - funktionel programmering paradigme
* **"Horizontal scale"** - kan skalere på tværs af flere servere

### Performance Issues Solutions
* **Performance issues - too many users** (no crazy kubernetes konfiguration)
* **Du kan bare få en større server** - vertikal skalering

### Core Technologies
* **Ecto** - database wrapper og query builder
* **Erlang VM** - runtime environment
* **Absinthe** - GraphQL implementation til Elixir
* **GraphQL** - query language til APIs
* **WebSocket** - real-time kommunikation

### Development Features
* **HEEx** - reusable components
* **Compiler Checks** - compile-time validering
* **Built-in Formatting** - automatisk kode formatering

## Server Monitoring
* **"Average memory used"** - hvor meget af serveren bruger du?
* **Scaling a server** - server skalering strategier

## Phoenix Routing

### Route Definition Eksempel
```elixir
get "/", PageController, :home
```

### Hvad betyder det:
* **get** - HTTP metode (GET request)
* **"/"** - URL path (hjemmesiden/root)
* **PageController** - Controller som skal håndtere requesten
* **:home** - Action/funktion i controlleren der skal kaldes

### Så når nogen:
1. Laver et GET request til / (hjemmesiden)
2. Kalder Phoenix PageController.home/2 funktionen
3. Som returnerer det HTML der skal vises

Det er Phoenix's måde at mappe URLs til kode på!

## Arity i Elixir

### /2 fortæller arity (antal argumenter)

**I Elixir betyder:**
* `PageController.home/2` = funktionen home med **2 argumenter**
* `/2` fortæller hvor mange parametre funktionen tager

### Phoenix Controller Actions

**Phoenix controller actions tager altid 2 argumenter:**
1. **conn** - connection struct (request info)
2. **params** - URL parametre og form data

## Sammenligning med Spring

### conn (Phoenix) ≈ HttpServletRequest + HttpServletResponse (Spring)
* Request headers, cookies, session
* HTTP metode, URL, query params
* Response funktioner

### params (Phoenix) ≈ @RequestParam + @PathVariable (Spring)
* URL parametre (?name=john)
* Path variables (/users/{id})
* Form data fra POST requests