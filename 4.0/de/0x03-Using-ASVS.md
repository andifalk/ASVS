# Verwendung des ASVS

Der ASVS verfolgt zwei Hauptziele:

* Organisationen bei der Entwicklung und Wartung sicherer Anwendungen zu unterstützen.
* Sicherheitsdienstleistern, Anbietern von Sicherheitswerkzeugen und Verbrauchern die Möglichkeit zu geben, deren Anforderungen und Angebote dazu aufeinander abzustimmen.

## Stufen des Application Security Verification Standards

Der Application Security Verification Standard definiert drei Verifizierungsstufen für Sicherheit, wobei jede Stufe immer weiter in die Tiefe geht.

* Die Stufe 1 ASVS ist für niedrige Sicherheitsstufen gedacht und ist vollständig durch Penetrationstests verifizierbar.
* Die Stufe 2 des ASVS ist für alle Anwendungen gedacht, die schützenwerte sensible Daten enthalten, und ist die empfohlene Stufe für die meisten Anwendungen.
* Die Stufe 3 des ASVS ist für die Anwendungen mit der höchsten Kritikalität gedacht - also Anwendungen, die Transaktionen von hohem Wert durchführen, sensible medizinische Daten enthalten bzw. alle Anwendungen, die ein Höchstmaß an Vertrauen erfordern.

Jede ASVS-Stufe enthält eine Liste von Sicherheitsanforderungen. Jede dieser Anforderungen kann auch auf sicherheitsspezifischen Features und Eigenschaften abgebildet werden, die von Entwicklern in die Software eingebaut werden müssen.

![ASVS Stufen](https://raw.githubusercontent.com/OWASP/ASVS/master/4.0/images/asvs_40_levels.png "ASVS Stufen")

Abbildung 1 - Stufen des OWASP Application Security Verification Standard 4.0

Die Stufe 1 ist die einzige Stufe, die vollständig von Menschen mittels Penetrationtests prüfbar ist. Alle anderen Stufen erfordern zusätzlich Zugang zu Dokumentation, Quellcode, Konfiguration und den am Entwicklungsprozess beteiligten Personen. Aber selbst wenn die Stufe 1 "Black Box"-Tests (ohne Dokumentation und Quellcode) zulässt, ist dies keine wirksame Sicherungsmaßnahme und es sollte proaktiv von deren alleinigen Verwendung abgeraten werden. Böswillige Angreifer haben sehr viel Zeit zur Verfügung, während für die meisten Penetrationstests nur ein paar Wochen zur Verfügung stehen. Die Verteidiger müssen Sicherheitskontrollen einbauen, alle Schwachstellen schützen, finden und beheben und böswillige Akteure innerhalb einer angemessenen Zeit aufspüren und darauf reagieren. Böswillige Akteure haben im Wesentlichen unendlich viel Zeit und benötigen nur eine einzige undichte Verteidigung, eine einzige Schwachstelle oder eine fehlende Erkennung, um erfolgreich zu sein. Black-Box-Tests, die hektisch oft erst am Ende der Entwicklung oder womöglich gar nicht durchgeführt werden, können dieser Asymmetrie unmöglich mit Erfolg begegnen.

In den letzten 30 Jahren haben Black-Box-Tests immer wieder bewiesen, daß dabei kritische Sicherheitsprobleme übersehen werden, die dann zu immer massiveren Verletzungen der Datensicherheit führen. Wir befürworten nachdrücklich den Einsatz einer breiten Palette von Verfahren zur Sicherheitssicherung und Verifizierungsmaßnahmen. Dies umfasst die Ablösung klassischer Penetrationstests durch quellcodegeführte (hybride) Penetrationstests auf Stufe 1, mit vollem Zugang zu den Entwicklern und der Dokumentation während des gesamten Entwicklungsprozesses. Die Finanzaufsichtsbehörden tolerieren keine externen Finanzprüfungen ohne Zugang zu den Bilanzbüchern, Mustertransaktionen oder den Personen, welche die Kontrollen durchführen. Industrie und Regierungen müssen den gleichen Standard an Transparenz im Bereich der Softwareentwicklung fordern.

Wir empfehlen nachdrücklich die Verwendung von Sicherheitswerkzeugen innerhalb des Entwicklungsprozesses. DAST- und SAST-Werkzeuge können von der Build-Pipeline kontinuierlich verwendet werden, um leicht zu aufzuspürende Sicherheitsprobleme, die niemals vorhanden sein sollten, zu finden ("Low Hanging Fruits").

Automatisierte Werkzeuge und Online-Scans können nicht mehr als die Hälfte der ASVS ohne menschliche Hilfe abdecken. Wenn eine umfassende Testautomatisierung für jeden Build erforderlich ist, dann wird eine Kombination aus benutzerdefinierten Unit- und Integrationstests zusammen mit durch den Build initiierten Online-Scans verwendet. Tests der Geschäftslogik und der Zugriffskontrolle sind nur mit menschlicher Unterstützung möglich. Diese sollten in Unit- und Integrationstests umgesetzt werden.

## Wie man diesen Standard verwendet

die beste Möglichkeit, den Application Security Verification Standard zu nutzen, ist diesen als Blaupause zur Erstellung einer Checkliste für die sichere Entwicklung zu verwenden, die speziell auf Ihre Anwendung, Plattform oder Organisation zugeschnitten ist. Durch die Anpassung des ASVS an Ihre Anwendungsfälle wird der Schwerpunkt auf die Sicherheitsanforderungen gelegt, die für Ihre Projekte und Umgebungen am wichtigsten sind.

### Stufe 1 - Erste Schritte - automatisiert und Ausgangspunkt für weitere Stufen

Eine Anwendung erreicht ASVS Stufe 1, wenn sie sich angemessen gegen einfach zu entdeckende Sicherheitslücken der Anwendung verteidigt, die in den OWASP Top 10 und anderen ähnlichen Checklisten beschrieben sind.

Die Stufe 1 ist das absolute Minimum, das alle Anwendungen anstreben sollten. Es ist auch hilfreich als erster Schritt innerhalb eines mehrstufigen Prozesses oder wenn Anwendungen keine sensiblen Daten speichern bzw. verarbeiten und daher nicht die strengeren Kontrollen der Stufen 2 oder 3 benötigen. Kontrollen der Stufe 1 können entweder automatisch durch Werkzeuge oder ohne großen Aufwand manuell ohne Zugriff auf den Quellcode überprüft werden. Wir betrachten Stufe 1 als das für alle Anwendungen erforderliche Minimum.

Bedrohungen für die Anwendung werden höchstwahrscheinlich von Angreifern ausgehen, die einfache wenig aufwendige Techniken verwenden, um schnell zu findende und leicht ausnutzbare Schwachstellen zu identifizieren. Dies steht im Gegensatz zu einem entschlossenen Angreifer, der seine Energie gezielt für die Anwendung einsetzt. Wenn die von Ihrer Anwendung verarbeiteten Daten einen hohen Wert haben, wird man nur selten mit einer Überprüfung der Stufe 1 aufhören.

### Stufe 2 - Der Standard für die meisten Anwendungen

Eine Anwendung erreicht ASVS Stufe 2 (d.h. den Standard), wenn sie die meisten Risiken, die heutzutage mit Software verbunden sind, angemessen abwehrt.

Stufe 2 stellt sicher, dass wirksame Sicherheitskontrollen vorhanden sind und innerhalb der Anwendung verwendet werden. Stufe 2 ist in der Regel für Anwendungen geeignet, die signifikante Business-zu-Business Transaktionen abwickeln. Einschließlich solcher, die Informationen aus dem Gesundheitswesen verarbeiten, geschäftskritische oder sensible Funktionen implementieren oder andere sensible Vermögenswerte verarbeiten, oder für Branchen, in denen die Integrität ein kritischer Aspekt zum Schutz ihres Geschäfts ist, wie z.B. die Spielindustrie, um Betrüger und Spiel-Hacks zu vereiteln.

Bedrohungen von Anwendungen der Stufe 2 sind in der Regel qualifizierte und motivierte Angreifer, die sich auf bestimmte Ziele konzentrieren und dabei Werkzeuge und Techniken einsetzen, die gut trainiert und wirksam sind, um Schwachstellen in Anwendungen zu entdecken und auszunutzen.

### Stufe 3 - Anwendungen mit sehr hohen Sicherheitsanforderungen

ASVS Stufe 3 ist die höchste Verifizierungsstufe innerhalb des ASVS. Diese Stufe ist in der Regel Anwendungen vorbehalten, die ein erhebliches Maß an Sicherheitsverifikation erfordern, wie z.B. solche, die in Bereichen des Militärs, der Gesundheit und Safety, kritischen Infrastrukturen usw. zu finden sind.

Für Organisationen kann die ASVS-Stufe 3 nötig werden, wenn deren Anwendungen kritische Funktionen ausführen, bei denen ein Ausfall die Operationen der Organisation und sogar ihre Überlebensfähigkeit erheblich beeinträchtigen könnte. Nachstehend finden Sie ein Beispiel für die Anwendung von ASVS Stufe 3. Eine Anwendung erreicht ASVS-Stufe 3 (Fortgeschrittene Stufe), wenn sie sich angemessen gegen fortgeschrittene Sicherheitslücken einer Anwendung wehrt und auch die Prinzipien eines guten Sicherheitsdesigns verfolgt.

Eine Anwendung auf ASVS-Stufe 3 erfordert eine gründlichere Analyse der Architektur, der Codierung und des Testprozesses als alle anderen Stufen. Eine sichere Anwendung wird auf sinnvolle Weise modularisiert (um die Robustheit, Skalierbarkeit und vor allem den Aufbau von Sicherheitsschichten zu erleichtern), und jedes Modul (getrennt nach Netzwerkverbindung und/oder physischer Instanz) kümmert sich um seine eigenen Sicherheitsverantwortlichkeiten (_Defense in Depth_), die angemessen dokumentiert werden müssen. Zu den Verantwortlichkeiten gehören Kontrollen zur Gewährleistung der Vertraulichkeit (z.B. Verschlüsselung), Integrität (z.B. Transaktionen, Eingabevalidierung), Verfügbarkeit (z.B. entsprechende Lastverteilung), Authentifizierung (auch zwischen Systemen), Unabstreitbarkeit, Autorisierung und Auditierung (Protokollierung).

## Anwendung des ASVS in der Praxis

Verschiedene Bedrohungen haben ihren Ursprung in unterschiedlichen Motivationen. Einige Branchen verfügen über einzigartige Informations- und Technologievorteile und bereichsspezifische regulatorische Anforderungen.

Organisationen wird empfohlen, ihre spezifischen Risikomerkmale auf der Grundlage ihrer Geschäftsart eingehend zu prüfen und auf Grundlage dieser Risiken und Geschäftsanforderungen die dafür geeignete ASVS-Ebene zu bestimmen.
