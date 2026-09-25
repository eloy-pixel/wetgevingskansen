# Wetgevingskansen

Elke week de kans dat een Nederlandse wet het haalt en op de geplande datum ingaat. Vooraf vastgelegd met een
onafhankelijk tijdstempel, en achteraf openbaar gescoord, ook als het fout zat.

## Waarom dit bestaat

Wie wil weten of een wet op 1 januari echt ingaat, leest nu Kamerstukken, de agenda van de Eerste Kamer en het
Staatsblad, en schat het daarna zelf in. Dit archief zet er een getal bij, en houdt bij hoe goed dat getal was. Een
voorspelling telt pas als ze er stond vóór de uitslag, dus elke ronde krijgt een tijdstempel dat niemand achteraf kan
verzetten.

## Hoe een ronde werkt

1. **De vraag.** Per wet één ja/nee-vraag met een vaste beslisregel. Bijvoorbeeld: treedt het hoofddeel van deze wet op
   1 januari 2027 in werking, volgens het Staatsblad en de officiële inwerkingtredingsbesluiten? Een latere datum,
   verwerping, intrekking of een ontbrekend besluit betekent nee.
2. **Het dossier.** Per wet worden de recente Nederlandse nieuwskoppen verzameld en ruw meegegeven, zonder samenvatting
   ertussen, samen met de stand van de wet op de dag van de ronde.
3. **De kans.** Eerst een basiskans zonder nieuws, zodat één opvallend bericht de uitkomst niet kaapt. Daarna oordelen
   drie verschillende taalmodellen los van elkaar. Hun kansen worden samengevoegd in logit-ruimte en begrensd tussen 2 en
   97 procent, want een zekere fout kost veel meer dan een zekere treffer oplevert.
4. **Het tijdstempel.** Elke ronde staat in `rondes/<datum>.json`. Van dat bestand gaat alleen de SHA-256 naar
   [freetsa.org](https://freetsa.org), die er een tijdstempel volgens RFC 3161 op zet. Het antwoord staat ernaast als
   `<datum>.json.tsr`. De leesversie, een tabel van hoog naar laag, staat in `rondes/<datum>.md`.
5. **De score.** Na de uitslag komt die bij de vraag te staan, met de Brier-score en de log-score, per wet en over alles.

## Zelf controleren

Download `cacert.pem` en `tsa.crt` van [freetsa.org/files](https://freetsa.org/files/) en draai:

```bash
openssl ts -verify -data rondes/2026-09-25.json -in rondes/2026-09-25.json.tsr -CAfile cacert.pem -untrusted tsa.crt
```

Staat er `Verification: OK`, dan bestond het bestand precies zo op het moment in het tijdstempel. Met
`openssl ts -reply -in rondes/2026-09-25.json.tsr -text` zie je dat moment.

## Wat dit niet is

Geen advies, geen weddenschap en geen inzet. Het zijn kansen, met de onderbouwing en de fouten erbij.

## Hergebruik

De gegevens in `rondes/` mogen vrij gebruikt worden onder [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.nl),
met een verwijzing naar dit archief.
