# Flask og Web Frameworks

## Hvad er Flask?

Flask er et letvægts webframework i Python, der bruges til at bygge webapplikationer og API'er.

Flask er et "microframework" i Python. Det giver dig de grundlæggende ting til at lave en webapp (routing, request/response, templates). Det er meget fleksibelt, fordi du selv kan tilføje databaser, autentificering osv. via udvidelser.

## Microframework vs Full-stack Framework

**Et microframework** er et lille, simpelt framework, der kun giver de mest nødvendige funktioner.

Det bruges ofte til små projekter, prototyper eller API'er, men kan også bruges til større systemer.

### Microframeworks (små, fleksible):
* **Flask** (Python)
* **FastAPI** (Python)
* **Bottle** (Python)
* **Sinatra** (Ruby)
* **Express.js** (JavaScript/Node.js)

### Full-stack frameworks (store, komplette):
* **Django** (Python)
* **Ruby on Rails** (Ruby)
* **Laravel** (PHP)
* **Spring** (Java)
* **ASP.NET MVC / Core** (C#)

## Rendering: Server-side vs Client-side

### Server-side rendering (MVC)
I klassisk **MVC med serverside rendering** (fx Spring MVC + Thymeleaf, eller Django + Jinja2):
* **Controlleren** henter data fra modellen
* **Viewet** (fx Thymeleaf-skabelon) bliver til en færdig HTML-side på serveren
* Browseren får ren HTML tilbage

### Client-side rendering (SPA)
Hvis du i stedet bruger **JavaScript frameworks** (fx React, Vue, Angular), så laver du oftest **client-side rendering** eller **SPA** (Single Page Application), hvor serveren sender data via et **REST API** eller **GraphQL**, og JavaScript bygger HTML i browseren.

**Sammenfatning:**
* **Thymeleaf → serverside rendering (MVC)**
* **JavaScript frameworks → clientside rendering (SPA)**

## Flask Grundkoncepter

### 1. Routing
Routing = "vejkortet" i en webapp.
* Fortæller hvilken funktion der skal køre, når en bestemt URL kaldes

### 2. Requests
Requests = de oplysninger browseren sender til serveren.
* Indeholder fx **metode** (GET, POST), **data** (formularinput, JSON) og **headers**

### 3. Templates
Templates = HTML-skabeloner med variabler og logik

## Web Servere og Application Servere

### Generelle webservere:
* **Apache HTTP Server**
* **Nginx**
* **Microsoft IIS**
* **Lighttpd**
* **Caddy**

### Java / Spring (Servlet-containere):
* **Apache Tomcat**
* **Jetty**
* **Undertow**
* **WildFly** (tidl. JBoss)
* **GlassFish / Payara**

### Python (via WSGI/ASGI):
* **Gunicorn**
* **uWSGI**
* **Daphne** (ASGI)
* **Hypercorn** (ASGI)

## Forskellen mellem Webserver og Applikationsserver

### Webserver (fx Nginx, Apache HTTP):
* Håndterer **HTTP-requests** direkte fra klienten
* Kan levere **statisk indhold** (HTML, billeder, CSS, JS)
* Kan videresende (proxy) requests til en applikationsserver
* Hurtig og effektiv til netværk, men **kører ikke din kode** (fx Java/Python)

### Applikationsserver (fx Tomcat, Gunicorn, uWSGI):
* Kører selve **din applikationskode** (Spring, Flask, Django)
* Forstår sprogspecifikke standarder:
  * Java → **Servlet API** (Tomcat, Jetty, Undertow)
  * Python → **WSGI/ASGI** (Gunicorn, uWSGI, Daphne)
* Returnerer svar til webserveren

### Typisk setup:
Browser → **Webserver (Nginx)** → **Applikationsserver (Tomcat/Gunicorn)** → **Din app**

## WSGI Standard

WSGI-standarden (Web Server Gateway Interface) er standarden for Python web applications.