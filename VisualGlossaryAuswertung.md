# Glossary Brief — Fahrrad-Sharing Visual Glossary

## 1. Transkription

**Begriffe (alle Stickies, exakte Schreibweise):**

```
Subscription, Commuter, APP, Customer Care Specialist,
Bestätigung, Reservierer, Fahrrad, Status,
Rack (mit Standort), blockiert, verfügbar, ausgeliehen, zurückgegeben
```

Alle Stickies sind einheitlich gelb — keine Piktogramm-Unterscheidung.

**Beziehungen (source → label → cardinality target):**

```
Commuter      —(anfrage)→           (no cardinality) Reservierer
Commuter      —(sucht)→             (no cardinality) Fahrrad
Commuter      —(has 1)→             1                APP
Commuter      —(unlabeled)→         0..*             Subscription
APP           —(unlabeled, ←)→      0 bis *          Subscription
Bestätigung   —(versendet an)→      (no cardinality) APP
Customer Care Specialist —(erzeugt / sendet)→ (no cardinality) Bestätigung
Reservierer   —(reserviert)→        (no cardinality) Fahrrad
Rack (mit Standort) —(unlabeled, ←)→ 0 bis *        Fahrrad
Fahrrad       —(has)→               (no cardinality) Status
Status        —(is ←)—              (no cardinality) blockiert
Status        —(is ←)—              (no cardinality) verfügbar
Status        —(unlabeled ←)—       (no cardinality) ausgeliehen
Status        —(unlabeled ←)—       (no cardinality) zurückgegeben
```

**Fan-out-Hinweis:** Status wird von vier Stickies (blockiert, verfügbar, ausgeliehen, zurückgegeben) mit eingehenden Pfeilen referenziert — das sind vier separate `is`-Beziehungen (Statuswerte), keine Aggregation.

---

## 2. Term-Katalog

| Term | Gloss | Auffälligkeiten |
|------|-------|----------------|
| **Commuter** | Endnutzer; bucht Subscription, sucht Fahrräder, nutzt APP | Kernakteur |
| **APP** | Mobile Anwendung; Kanal zwischen Commuter und System | UI-Oberfläche, kein Datenbehälter |
| **Subscription** | Abonnement-Vertrag des Commuters | Verbunden mit Commuter und APP — zwei eingehende Kanten, Semantik unklar |
| **Customer Care Specialist** | Support-Rolle; erzeugt und sendet Bestätigungen | Einziger interner Akteur neben Reservierer |
| **Bestätigung** | Rückmeldung auf eine Subscription-Buchung | Nur ausgehend an APP; kein Attribut sichtbar |
| **Reservierer** | System, das Fahrräder reserviert/blockiert | Software-System (kein Mensch); erhält Anfragen vom Commuter |
| **Fahrrad** | Das zu verleihende Objekt | Kernentität; hat Status, liegt in Rack |
| **Status** | Zustandswert eines Fahrrads | Vier eingehende `is`-Kanten → dies ist eine Enumeration, kein eigenständiges Objekt |
| **Rack (mit Standort)** | Physischer Abstellort mit Geo-Information | `0..*` Fahrrads pro Rack |
| **blockiert** | Statuswert: Fahrrad reserviert, noch nicht übernommen | Statusausprägung |
| **verfügbar** | Statuswert: Fahrrad bereit zur Buchung | Statusausprägung |
| **ausgeliehen** | Statuswert: Fahrrad gerade in Benutzung | Statusausprägung |
| **zurückgegeben** | Statuswert: Fahrrad zurück im Rack, noch nicht freigegeben | Statusausprägung |

---

## 3. Beziehungstabelle

| Source | Label | Target | Kardinalität (angegeben) | Inverse (nicht angegeben) | Art |
|--------|-------|--------|--------------------------|--------------------------|-----|
| Commuter | anfrage | Reservierer | keine | keine | Assoziation |
| Commuter | sucht | Fahrrad | keine | keine | Assoziation |
| Commuter | has | APP | 1 | keine | Komposition? |
| Commuter | (unlabeled) | Subscription | 0..* | keine | Assoziation |
| APP | (unlabeled) | Subscription | 0 bis * | keine | Assoziation |
| Customer Care Specialist | erzeugt / sendet | Bestätigung | keine | keine | Assoziation |
| Bestätigung | versendet an | APP | keine | keine | Assoziation |
| Reservierer | reserviert | Fahrrad | keine | keine | Assoziation |
| Rack (mit Standort) | (unlabeled) | Fahrrad | 0 bis * | keine | Komposition |
| Fahrrad | has | Status | keine | keine | Komposition |
| blockiert | is | Status | keine | — | Enumeration |
| verfügbar | is | Status | keine | — | Enumeration |
| ausgeliehen | (unlabeled) | Status | keine | — | Enumeration |
| zurückgegeben | (unlabeled) | Status | keine | — | Enumeration |

**Auffälligkeit:** Zwei Kanten laufen in `Subscription` ein (von Commuter und von APP) — unklar ob das dieselbe Beziehung aus zwei Perspektiven ist oder zwei verschiedene.

---

## 4. Abgeleitetes Domänenmodell

*(Explizit als Ableitung markiert — Abweichungen von der Darstellung sind Urteilsentscheide)*

**Entitäten:**

| Entität | Identity | Attribute (erschlossen) |
|---------|----------|------------------------|
| **Commuter** | commuter_id | name, kontakt |
| **Fahrrad** | fahrrad_id | status (Enum), rack_id |
| **Subscription** | subscription_id | commuter_id, status, start_date |
| **Rack** | rack_id | standort (Koordinaten/Adresse) |
| **Bestätigung** | bestätigung_id | subscription_id, sent_at |

**Value Objects:**

| Value Object | Teil von | Begründung |
|-------------|----------|-----------|
| **Status** | Fahrrad | Enumeration ohne eigene Identität: `verfügbar`, `blockiert`, `ausgeliehen`, `zurückgegeben` |

**Software-Systeme (keine Entitäten):**

- **APP** — UI-Kanal
- **Reservierer** — internes Subsystem/Service

**Akteure (keine Entitäten):**

- **Customer Care Specialist** — Benutzerrolle

**Aggregate (Urteilsentscheid):**

- `Fahrrad` ist Aggregate Root — besitzt Status, gehört zu Rack
- `Commuter` ist Aggregate Root — besitzt Subscription(s), hat APP

---

## 5. Business Rules aus dem Glossar

| Regel | Quelle |
|-------|--------|
| Ein Commuter hat genau **1** APP | `Commuter has 1 APP` |
| Ein Commuter kann **0 bis viele** Subscriptions haben | `Commuter → 0..* Subscription` |
| Ein Rack enthält **0 bis viele** Fahrräder | `Rack → 0 bis * Fahrrad` |
| Ein Fahrrad hat **genau einen** Status zu jedem Zeitpunkt | `Fahrrad has Status` + vier `is`-Kanten |
| Gültige Statuswerte: `verfügbar`, `blockiert`, `ausgeliehen`, `zurückgegeben` | Status-Stickies |

---

## 6. Bounded Contexts / Gruppierung

Keine Gruppen oder Lanes im Glossar. Natürliche Clusterung (Vorschlag):

| Cluster | Begriffe |
|---------|---------|
| **Nutzer & Zugang** | Commuter, APP, Subscription, Bestätigung, Customer Care Specialist |
| **Fahrzeug & Logistik** | Fahrrad, Status, Rack (mit Standort), Reservierer |

Passt zur Domain Story Auswertung: *Onboarding/Subscription* vs. *Bike Lifecycle*.

---

## 7. Offene Fragen (priorisiert)

| # | Frage |
|---|-------|
| 1 | **Zwei Kanten zu Subscription:** Commuter und APP zeigen beide `0..*` auf Subscription — ist das dieselbe Beziehung aus zwei Richtungen, oder kann eine Subscription ohne Commuter existieren (z.B. Firmen-Account über APP)? |
| 2 | **Inverse Kardinalitäten fehlen überall:** Wie viele Commuter kann ein Rack bedienen? Wie viele Subscriptions darf ein Commuter gleichzeitig haben? Wie viele Fahrrads darf ein Commuter gleichzeitig reservieren? |
| 3 | **Status `ausgeliehen` und `zurückgegeben` ohne Label:** Zwei der vier Status-Stickies haben keinen `is`-Label. Ist das eine Notationslücke oder eine andere Beziehungsart? |
| 4 | **Reservierer als System oder Rolle?** Der Reservierer erhält Anfragen und reserviert — ist das ein separater Service, ein Teil der APP, oder ein manueller Schritt? |
| 5 | **Bestätigung ohne Kardinalität:** Wie viele Bestätigungen gehören zu einer Subscription — genau eine, oder können Folgebestätigungen entstehen? |
| 6 | **Commuter has 1 APP:** Ist die APP eine Instanz (konkrete App-Installation) oder eine Klasse? Bedeutet `1`, dass Multi-Device-Nutzung nicht vorgesehen ist? |
| 7 | **Fahrrad-Identität:** Über welches Attribut wird ein Fahrrad eindeutig identifiziert — Serien-Nr., QR-Code, NFC-Tag? Nicht im Glossar. |
| 8 | **Rack ohne Verb zu Fahrrad:** Die Kante `Rack → 0 bis * Fahrrad` fehlt ein Verb — ist das `contains`, `stores`, etwas anderes? |
