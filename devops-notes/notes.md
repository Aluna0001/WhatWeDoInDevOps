#konventioner

#GitHub Marketplace

#"Langsomt erstatte routes"

#APIspec

#"We will work with environment variables defined in config files called dotenv. Dotenv exists across many languages. The standard is that the files are named .env"

#".env tæt på metal or not"

# Swagger og API Dokumentation

## Hvad er Swagger?

Swagger er et værktøj og en standard til at beskrive og dokumentere REST API'er. Det gør det nemt for udviklere at forstå, teste og arbejde med API'er uden at skulle læse hele kildekoden eller manualer.

## Hovedfunktioner

* **Swagger = Dokumentation + Interaktiv test af API'er**
* Bruger OpenAPI-specifikationen (tidligere kaldet Swagger-specifikationen)
* Se og prøv API-endpoints direkte i en browser med Swagger UI
* Hjælper både backend- og frontend-udviklere med at samarbejde mere effektivt

## Hvad er Schemas?

* **Schema = En model eller struktur for data**
* Definerer hvilke felter et objekt har, hvilke typer de er (string, number, boolean, array osv.), og om de er påkrævede
* Bruges til:
    * Input/output validering
    * Tydelig API dokumentation


#Commit often

# Call Hierarki

## Hvad betyder call hierarki?

En **call hierarki** (eller kaldhierarki) er en oversigt over, hvordan metoder (eller funktioner) kalder hinanden i et program.

Det hjælper med at forstå **hvem der kalder hvem**, og i hvilken rækkefølge tingene bliver udført.

## To vinkler på call hierarki:

1. **Callers** – Hvilke metoder kalder denne metode?
2. **Callees** – Hvilke metoder bliver kaldt *af* denne metode?

## Hvorfor er det nyttigt?

* **Fejlsøgning:** Man kan følge "call stack" og se, hvor en fejl stammer fra
* **Forståelse:** Når man overtager kode, kan man se, hvordan logikken hænger sammen
* **Performance-optimering:** Find ud af, hvilke metoder der bliver kaldt (måske alt for mange gange)
* **IDE-support:** I fx IntelliJ, Eclipse, eller Visual Studio kan man højreklikke på en metode og vælge *Show Call Hierarchy*, så man ser en grafisk oversigt
