## NoSQL

### Några olika typer av NoSQL:
- Document
- Key-value
- Graph
- Column

----

### Key-Value
Den enklaste typen av NoSQL.<br>
All data lagras som ett par, Key & Value.<br>
_Kan liknas vid ett lexikon._
#### Key _(Nyckel)_<br>
Varje Key måste vara unik då den används för att identifiera varje individuellt Value.<br>
Kan vara, nästan, vad som helst; beroende på eventuella restriktioner från programvaran.
#### Value _(Värde)_<br>
Value är datan som lagras, alternativt en referens till den plats där datan lagras.<br>
Kan vara allt från en textsträng, lista, ett Key-Value par till ett objekt.<br>
Vissa programvaror tillåter att användaren specificerar datatypen för Value.

>#### Kort summering:
>- Data lagras som par.
>- Key - Unikt värde för att identifiera tillhörande Value.
>- Value - Data som lagras, alt. en referens till lagring av data.<br>
>- Value kan var allt från en textsträng till ytterligare Key-Value par.

  #### Exempel på användningsområden:
- _**Webbapplikationer**_
  - **Key:** Session_id
  - **Value:** Användarens preferenser
- _**Aktiekurser**_
  - **Key:** Namn
  - **Value:** Aktuellt kursvärde
- _**Telefonbok**_
  - **Key:** Namn
  - **Value:** Telefonnummer
- _**Bilregister**_
  - **Key:** Registreringsnummer
  - **Value:** Datum för besiktning

#### Verkliga exempel:
>Twitter: Cache för sin timeline.<br>
>Coinbase: Säkerställa Bitcoin transaktioner.<br>
>Pintrest: Lagra information om följare, boards m.m.<br>

![Key-Value databas][KeyValue]

Ett nyckel/värde-lager är i grunden en stor hash-tabell. Du kopplar varje datavärde till en unik nyckel och nyckel/värde-lagret använder den här nyckeln för att lagra data med hjälp av en lämplig hash-funktion. Hash-funktionen väljs för att tillhandahålla en jämn fördelning av hash-formaterade nycklar i datalagringen.

De flesta nyckel/värde-lager har endast stöd för enkla fråge-, infognings- och borttagningsåtgärder. För att ändra ett värde (delvis eller helt) måste ett program skriva över befintliga data för hela värdet. I de flesta implementeringar är läsning eller skrivning av ett enskilt värde en atomisk åtgärd. Om värdet är stort kan det ta lite tid att skriva.

Ett program kan lagra valfria data som en värdeuppsättning, även om vissa nyckel/värde-lager har gränser för den högsta storleken på värden. De lagrade värdena är täckande för lagringssystemets programvara. All schemainformation måste anges och tolkas av programmet. Värden är i princip blobar och nyckel/värde-lagret hämtar eller lagrar helt enkelt värdet efter nyckel.

Exempel på data i ett nyckel/värde-lager

Nyckel/värde-lager är mycket optimerade för program som utför enkla uppslag med hjälp av nyckelns värde eller med ett antal nycklar, men är mindre lämpliga för system som behöver fråga efter data i olika tabeller med nycklar/värden, till exempel att koppla data över flera tabeller.

Nyckel/värde-lager är inte heller optimerade för scenarier där frågor eller filtrering efter icke-nyckelvärden är viktigt, i stället för att utföra uppslag som endast baseras på nycklar. Med en relationsdatabas kan du till exempel hitta en post med hjälp av en WHERE-sats för att filtrera kolumner som inte är nyckelkolumner, men nyckel/värde-lager har vanligtvis inte den här typen av sökningsfunktion för värden, eller om de gör det krävs en långsam genomsökning av alla värden.

Ett enda nyckel/värde-lager kan vara extremt skalbart, eftersom datalagret enkelt kan distribuera data över flera noder på separata datorer.

----

### Column

En kolumndatabas ordnar data i kolumner och rader.<br> 
I sin enklaste form kan ett kolumnfamiljedatalager likna en relationsdatabas, åtminstone konceptuellt. Den verkliga kraften hos en kolumnfamiljedatabas ligger i dess avormaliserade metod för att strukturera glesa data, som kommer från den kolumnorienterade metoden för att lagra data.

Du kan tänka på ett kolumnfamiljedatalager som att det innehåller tabelldata med rader och kolumner, men kolumnerna är indelade i grupper som kallas kolumnfamiljer. Varje kolumnfamilj innehåller en uppsättning kolumner som är logiskt relaterade och som vanligtvis hämtas eller ändras som en enhet. Andra data som kan nås separat kan lagras i separata kolumnserier. I en kolumnserie kan nya kolumner läggas till dynamiskt, och rader kan vara null-optimerade (dvs. en rad behöver inte ha ett värde för varje kolumn).

Till skillnad från ett nyckel/värde-lager eller en dokumentdatabas lagrar de flesta kolumnfamiljedatabaser data fysiskt i nyckelordning, i stället för att beräkna en hash. Radnyckeln anses vara det primära indexet och möjliggör nyckelbaserad åtkomst via en specifik nyckel eller ett intervall med nycklar. Med vissa implementeringar kan du skapa sekundära index över specifika kolumner i en kolumnfamilj. Med sekundära index kan du hämta data efter kolumnvärde i stället för radnyckel.

På disk lagras alla kolumner i en kolumnfamilj tillsammans i samma fil, med ett visst antal rader i varje fil. Med stora datamängder skapar den här metoden en prestandaförmån genom att minska mängden data som behöver läsas från disken när endast ett fåtal kolumner efterfrågas tillsammans åt gången.

Läs- och skrivåtgärder för en rad är vanligtvis atomiska inom en enda kolumnfamilj, även om vissa implementeringar ger atomicitet över hela raden som sträcker sig över flera kolumnfamiljer.

----

### Document

Istället för att använda ett databasschema för att designa databasen (vilket man gör med relationsdatabaser) används dokument för att beskriva vilken data som ska lagras i dokumentdatabasen. 

Förutom att definiera datan och dess struktur så används dokument också för att lagra data, det istället för tabeller med kolumner och rader. En unik nykel tillhör varje dokument, den används för att hämta dokumentet ur databasen. 

Enkelt förklarat kan man likna dokument i dokumentdatabaser vid objekt i programmeringens värld.

Dokumentdatabaser låter oss nästla relaterad data i ett enda dokument _(en enda datastruktur)_ istället för att dela upp den i olika tabeller.
Varje dokument består av par av fält och värden. Det kan vara olika typer som t.ex. strings, booleans, arrays, objects, etc.

Uppstod när behovet att undvika data-duplicering slutade vara lika stort. No-SQL-databaser kan ur ett perspektiv anses göra det enklare för programmerare/systemutvecklare att arbeta med datalagring eftersom strukturen på datan bättre överensstämmer med hur man oftast hanterar data i programmeringskod. Det innebär att det ofta inte blir lika mycket jobb med att hantera mappningen av datan från databasen till källkoden och vice versa.

Låter oss lagra stora datamängder på ett enklare sätt, exempel: användarprofiler, Content management system, etc.



>#### Kort summering:
>- Data lagras i flexibla "dokument".
>- .json liknande format.
>- Innehållet i varje dokument kan variera beroende på behovet.
>- Datastrukturen kan förändras.
>- Mappar data mot objekt i applikationer.
>- Flexibelt och skalbart.

Ett dokumentdatalager hanterar en uppsättning namngivna strängfält och objektdatavärden i en entitet som kallas ett dokument. Dessa datalager lagrar vanligtvis data i form av JSON-dokument. Varje fältvärde kan vara ett skalära objekt, till exempel ett tal eller ett sammansatt element, till exempel en lista eller en överordnad-underordnad samling. Data i fälten i ett dokument kan kodas på en mängd olika sätt, inklusive XML, YAML, JSON, BSON eller till och med lagras som oformaterad text. Fälten i dokumenten exponeras för lagringshanteringssystemet, vilket gör det möjligt för ett program att fråga efter och filtrera data med hjälp av värdena i dessa fält.

Ett dokument innehåller vanligtvis alla data för en entitet. De objekt som utgör en entitet varierar beroende på tillämpningen. En entitet kan till exempel innehålla information om en kund, en order eller en kombination av båda. Ett enda dokument kan innehålla information som skulle vara utspridd över flera relationstabeller i ett hanteringssystem för relationsdatabaser (RDBMS). Dokumentarkiv kräver inte att alla dokument har samma struktur. Den här metoden med fri form ger stor flexibilitet. Program kan till exempel lagra olika data i dokument som svar på ändringar i affärskraven.

Exempeldokumentdatalager

Programmet kan hämta dokument med hjälp av dokumentnyckeln. Det här är en unik identifierare för dokumentet, som ofta är hash-formaterat, som hjälper till att fördela data jämnt. Vissa dokumentdatabaser skapar dokumentnyckeln automatiskt. Andra gör att du kan ange ett attribut för det dokument som ska användas som nyckel. Programmet kan även köra frågor mot dokument baserat på värdet för ett eller flera fält. Vissa dokumentdatabaser stöder indexering för att underlätta snabb sökning efter dokument baserat på ett eller flera indexerade fält.

Många dokumentdatabaser har stöd för uppdateringar på plats, vilket gör det möjligt för ett program att ändra värdena i specifika fält i ett dokument utan att skriva om hela dokumentet. Läs- och skrivåtgärder över flera fält i ett enda dokument är vanligtvis atomiska.

----

### Graph

Ett diagramdatalager hanterar två typer av information, noder och kanter. Noder representerar entiteter och kanter anger relationerna mellan dessa entiteter. Både noder och kanter kan ha egenskaper som ger information om den noden eller kanten, vilket liknar kolumner i en tabell. Kanter kan också ha en riktning som visar relationens typ.

Syftet med ett grafdatalager är att ett program effektivt ska kunna köra frågor som passerar nätverket med noder och kanter och analysera relationerna mellan entiteter. Följande diagram visar en organisations personaldata strukturerade som ett diagram. Entiteterna är medarbetare och avdelningar, och kanterna visar rapportförhållanden samt den avdelning där medarbetarna arbetar. I den här grafen visar pilarna vid kanterna riktningen för relationerna.

Exempel på data i ett diagramdatalager

Den här strukturen gör det enkelt att köra frågor som "Hitta alla medarbetare som rapporterar direkt eller indirekt till Sarah" eller "Vem arbetar på samma avdelning som John?" För stora grafer med många entiteter och relationer kan du utföra komplexa analyser snabbt. Många grafdatabaser ger ett frågespråk som du kan använda för att gå igenom ett nätverk med relationer på ett effektivt sätt.

----

### Collection
- NoSQL's version av tabeller.
- Behöver inte schema.
  - Behöver inte samma fält och/eller struktur.
  - Anpassas efter användarens behov
  - Kombinera objekt om dem ska användas tillsammans.
  - Använd aggregation.
  - Join vid insert men bör inte användas vid select.

----

### Exempel - Blogg
- Varje post ska ha title, description och URL.
- Varje post kan ha en eller flera taggar.
- Varje post ska ha namnet på den som skrev det, samt totalt antal likes.
- Varje post kan ha kommentarer, 0-*.
  - Dessa ska innehålla 
    - Användarnamn
    - Kommentar
    - Tidpunkt
    - Likes

---

#### Relationsdatabas (T.ex. MySQL)

![Relationell tabell][SQLTables]

- 3 tabeller
  - **Kommentarer**
    - Comment_id
      - Kommentarens unika id
    - Post_id
      - Id för det inlägg som kommentaren tillhör
    - By_user
      - Vilken användare som skrev kommentaren
    - Message
      - Den text som kommentaren består av
    - Data_time
      - Tidpunkt som kommentaren skrevs
    - likes
      - Antal likes som kommentaren har fått
  - **Posts**
    - id
      - Inläggets unika id
    - title
      - Inläggets titel
    - description
      - Beskrivning av inlägget
    - url
      - Länk till inlägget
    - likes
      - Antal likes som inlägget har fått
    - Post_by
      - Vem som postade inlägget
  - **Taggar**
    - id
      - Taggens unika id
    - Post_id
      - Id för det inlägg som taggen tillhör
    - tag
      - Den text som taggen består av

---

#### Dokumentdatabas (T.ex. MongoDB)

```json
  {
  "_id": "POST_ID",                   // Inläggets unika id
  "title": "TITLE_OF_POST",           // Inläggets titel
  "description": "POST_DESCRIPTION",  // Beskrivning av inlägget
  "by": "POST_BY",                    // Vem som postade inlägget
  "url": "URL_OF_POST",               // Länk till inlägget
  "tags": "[TAG1, TAG2, TAG3]",       // Taggar som hör till inlägget
  "likes": "TOTAL_LIKES",             // Antal likes som inlägget har fått
  "comments": [                       // En samling av eventuella kommentarer
    {
      "user": "COMMENT_BY",           // Vilken användare som skrev kommentaren
      "message": "TEXT",              // Den text som kommentaren består av
      "dateCreated": "DATE_TIME",     // Tidpunkt som kommentaren skrevs
      "like": "LIKES"                 // Antal likes som kommentaren har fått
    },
    {
      "user": "COMMENT_BY",           // Vilken användare som skrev kommentaren
      "message": "TEXT",              // Den text som kommentaren består av
      "dateCreated": "DATE_TIME",     // Tidpunkt som kommentaren skrevs
      "like": "LIKES"                 // Antal likes som kommentaren har fått
    }
  ]
}
```

- En collection istället för 3 tabeller.
  - **Post**
  - All data lagras i samma "dokument".
  - Allt hör till samma post och behöver inte användas på flera ställen.
  - En kommentar hör till exemepel till en specifik post.
    - Ingen annat dokument behöver innehålla den specifika kommentaren.



### Exempel på dokumentstruktur

Inleds och avslutas med curly brackets { }


[KeyValue]: /images/KeyValue.png
[SQLTables]: /images/SQLoverview.png

