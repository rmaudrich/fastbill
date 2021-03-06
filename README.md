#Fastbill

Dies ist eine kleine Library um mittels PHP mit der Fastbill API kommunizieren zu können.
So können Sie mit wenigen Schritten und wenig Vorkenntnissen auf Ihre Fastbill-Daten zugreifen und diese verarbeiten. 

In der [Fastbill-API Dokumentation](http://www.fastbill.com/api/ "Fastbill API Dokumentation") finden Sie die Struktur der einzelnen Requests. Diese müssen in Form von Arrays an die Klasse übergeben werden. Am einfachsten ist es, sich an die **Request - JSON** Beispiele aus der Dokumentation zu halten.



##Installation

Binden Sie die aktuellste Version ein und initialisieren Sie die fastbill-Klasse mit Ihrer Fastbill-Email und APIKey.

``` php
require("fastbill.x.x.php");
$fastbill = new fastbill("%Fastbill-Email%", "%Fastbill-APIKey%");
```
Ersetzen Sie <code>%Fastbill-Email%</code> durch Ihre Fastbill-E-Mail-Adresse (z.B. *max@mustermann.de*) und <code>%Fastbill-APIKey%</code> durch Ihren Fastbill-APIKey (z.B. *1238751bd8714ciafnafv3afubafeGizQnudJHBzfaiusbwt48*). Sollten Sie die Parameter vergessen oder diese Leer sein gibt <code>new fastbill()</code> *False* zurück.



##Klassen

``` php
$fastbill->request();
```
Diese Klasse erwartet ein Array mit den Request Daten: *Service, Filter, Limit, Offset* und *Data*.
Als Rückgabe erhalten Sie die Fastbill Antwort in einem Array.
Sollte es zu Fehlern kommen, erhalten Sie als Rückgabe *False*.



##Beispiele


Hier ein Beispiel für Rechnungen:
``` php
// Als Rückgabe erhalten Sie alle Rechnungen
$temp = $fastbill->request(array("SERVICE" => "invoice.get"));
print_r($temp);

// Hier alle Ausgangsrechnungen
$temp = $fastbill->request(array("SERVICE" => "invoice.get", "FILTER" => array("TYPE" => "outgoing")));
print_r($temp);

// Und hier die ersten drei Ausgangsrechnungen
$temp = $fastbill->request(array("SERVICE" => "invoice.get", "FILTER" => array("TYPE" => "outgoing"), "LIMIT" => 3));
print_r($temp);
```

Hier ein Beispiel für Kunden:
``` php
// Als Rückgabe erhalten Sie alle Kunden
$temp = $fastbill->request(array("SERVICE" => "customer.get"));
print_r($temp);

// Hier den Kunden mit der ID 5376
$temp = $fastbill->request(array("SERVICE" => "invoice.get", "FILTER" => array("CUSTOMER_ID" => 5376)));
print_r($temp);
```

