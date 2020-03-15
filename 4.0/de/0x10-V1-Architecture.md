# V1: Anforderungen für Architektur, Design und die Bedrohungsmodellierung

## Zielsetzung

Die Sicherheitsarchitektur ist in vielen Organisationen fast zu einer verschollenen Kunst verkommen. Die Tage des Enterprisearchitekten sind im Zeitalter von DevSecOps größtenteils vorbei. Der Bereich der Anwendungssicherheit muss hier verlorenes Terrain aufholen, agile Sicherheitsprinzipien übernehmen und gleichzeitig anerkannte sichere Architekturprinzipien wieder in die Software-Praxis einführen. Architektur ist nicht die Implementierung, sondern die Art und Weise, über ein Problem nachzudenken, das potenziell viele verschiedene Lösungsmöglichkeiten hat, und nicht nur eine einzige "richtige" Antwort besitzt. Nur allzu oft wird gerade die Sicherheit als unflexibel angesehen und verlangt von den Entwicklern, Code auf eine bestimmte Art und Weise zu reparieren, obwohl die Entwickler vielleicht eine viel bessere Möglichkeit kennen, das Problem zu lösen. Es gibt nicht die eine einfache Lösung für die Architektur, und so zu tun, als ob es nicht so wäre, ist ein Bärendienst für die Softwareentwicklung.

Eine spezifische Implementierung einer Webanwendung wird wahrscheinlich während ihrer gesamten Lebensdauer kontinuierlich überarbeitet, die Gesamtarchitektur wird sich dagegen nur selten ändern, sondern sich eher langsam weiter entwickeln. Eine Sicherheitsarchitektur unterscheidet sich hier nicht - wir brauchen heute eine Authentifizierung, wir werden morgen eine Authentifizierung benötigen, und wir werden sie in fünf Jahren brauchen. Wenn wir heute fundierte Entscheidungen treffen, können wir viel Aufwand, Zeit und Geld sparen, wenn wir architekturkonforme Lösungen auswählen und wiederverwenden. Vor einem Jahrzehnt beispielsweise wurde die Multi-Faktor-Authentifizierung nur selten implementiert.

Hätten Entwickler in ein einziges, sicheres Identitätsprovider-Modell investiert, wie z.B. eine föderierte SAML-Identität, könnte der Identitätsprovider einfach aktualisiert werden, um neue Anforderungen wie die NIST 800-63-Konformität einzubeziehen, ohne die Schnittstellen der ursprünglichen Anwendung zu ändern. Immer wenn viele Anwendungen die gleiche Sicherheitsarchitektur und damit die gleiche Komponente nutzen, profitieren sie alle gleichzeitig von diesem Upgrade. SAML wird jedoch nicht immer die beste oder geeignetste Authentifizierungslösung bleiben - es muss möglicherweise gegen andere Lösungen wie z.B. OpenID Connect ausgetauscht werden, wenn sich die Anforderungen ändern. Änderungen wie diese sind entweder kompliziert, so kostspielig, dass eine komplette Neuentwicklung erforderlich ist, oder ohne eine Sicherheitsarchitektur schlichtweg unmöglich.

In diesem Kapitel behandelt der ASVS die wichtigsten Aspekte jeder soliden Sicherheitsarchitektur:

* Verfügbarkeit
* Vertraulichkeit
* Verarbeitungsintegrität
* Nichtabstreitbarkeit
* Datenschutz

Alle dieser Sicherheitsprinzipien müssen als Bestandteil in allen Anwendungen integriert sein. Ein _Shift-Left_ ist entscheidend, beginnend mit der Befähigung der Entwickler durch Checklisten für die sichere Kodierung, Mentoring und Schulungen, Kodierung und Tests, Aufbau, Bereitstellung, Konfiguration und Betrieb und endend mit unabhängigen Tests, um sicherzustellen, dass alle Sicherheitskontrollen vorhanden und funktionsfähig sind. Früher war der letzte Testschritt alles, was wir als Industrieunternehmen umgesetzt haben, aber das reicht nicht mehr aus, wenn Entwickler zehn- oder hundertmal am Tag Code in die Produktion schieben. Anwendungssicherheitsexperten müssen mit agilen Techniken Schritt halten. Das bedeutet, dass sie Entwicklerwerkzeuge einsetzen, den Code lernen und mit den Entwicklern zusammenarbeiten müssen, anstatt das Projekt monatelang mit Sicherheitsblockaden zu überhäufen, während alle anderen Projektbeteiligten längst weiter gearbeitet haben.

## V1.1 Anforderungen an einen sicheren Softwareentwicklungslebenszyklus

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.1.1** | Überprüfen Sie die Verwendung eines sicheren Softwareentwicklungslebenszyklus, der die Sicherheit in allen Entwicklungsphasen berücksichtigt. ([C1](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | |
| **1.1.2** | Überprüfen Sie bei jeder Designänderung oder Sprintplanung den Einsatz von Bedrohungsmodellen (_threat models_), um Bedrohungen zu identifizieren, Gegenmaßnahmen zu planen, angemessene Reaktionen auf Risiken zu erleichtern und Sicherheitstests anzuleiten. | | ✓ | ✓ | 1053 |
| **1.1.3** | Vergewissern Sie sich, dass alle Userstories und Features funktionale Sicherheitseinschränkungen enthalten, wie z.B. _Als Benutzer sollte ich mein Profil anzeigen und bearbeiten können. Ich sollte nicht in der Lage sein, das Profil anderer Personen anzuzeigen oder zu bearbeiten_.
 |  | ✓ | ✓ | 1110 |
| **1.1.4** | Überprüfen Sie die Dokumentation und Begründung aller Vertrauensgrenzen, Komponenten und wichtigen Datenflüsse der Anwendung. | | ✓ | ✓ | 1059 |
| **1.1.5** | Überprüfen Sie die Definition und Sicherheitsanalyse der High-Level-Architektur der Anwendung und aller angeschlossenen Remotedienste. ([C1](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 1059 |
| **1.1.6** | Überprüfen Sie die Implementierung zentralisierter, einfacher (Wirtschaftlichkeit des Designs), geprüfter, sicherer und wiederverwendbarer Sicherheitskontrollen, um doppelte, fehlende, unwirksame oder unsichere Kontrollen zu vermeiden. ([C10](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 637 |
| **1.1.7** | Überprüfen Sie die Verfügbarkeit einer Checkliste für sichere Kodierung, Sicherheitsanforderungen, von Leitfäden oder Richtlinien für alle Entwickler und Tester. | | ✓ | ✓ | 637 |

## V1.2 Anforderungen an die Authentifizierungsarchitektur

Beim Entwurf der Authentifizierung spielt es keine Rolle, ob Sie über eine starke, hardwarebasierte Multi-Faktor-Authentifizierung verfügen, wenn ein Angreifer gleichzeitig ein Konto zurücksetzen kann, indem er lediglich ein Callcenter anruft und allgemein bekannte Fragen beantwortet. Beim Identitätsnachweis müssen __alle__ Authentifizierungswege die gleiche Stärke aufweisen.

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.2.1** | Überprüfen Sie, ob die Kommunikation zwischen Anwendungskomponenten, einschließlich APIs, Middleware und Datenschichten, authentifiziert ist und individuelle Benutzerkonten verwendet. ([C3](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 306 |
| **1.2.2** | Vergewissern Sie sich, dass die Anwendung einen einzigen geprüften Authentifizierungsmechanismus verwendet, der bekanntermaßen sicher ist, auf eine stärkere Authentifizierung ausgedehnt werden kann und über eine ausreichende Protokollierung und Überwachung verfügt, um Kontomissbrauch oder -verletzungen zu erkennen.
 | | ✓ | ✓ | 306 |
| **1.2.3** | Vergewissern Sie sich, dass alle Authentifizierungspfade und Identitätsmanagement-APIs eine einheitliche Stärke der Authentifizierungssicherheitskontrolle implementieren, so dass es keine schwächeren Alternativen für das Risiko der Anwendung gibt.

 | | ✓ | ✓ | 306 |

## V1.3 Architektonische Anforderungen an das Sitzungsmanagement

Dies dient als ein Platzhalter für zukünftige architektonische Anforderungen.

## V1.4 Anforderungen an die Architektur der Zugriffskontrolle

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.4.1** | Vergewissern Sie sich, dass vertrauenswürdige Durchsetzungspunkte, z.B. an Gateways für Zugangskontrolle, Servern und _serverlosen_ Funktionen, die Zugangskontrollen durchsetzen. Setzen Sie niemals Zugriffskontrollen nur auf dem Client durch. | | ✓ | ✓ | 602 |
| **1.4.2** | Überprüfen Sie, ob die gewählte Lösung zur Zugangskontrolle flexibel genug ist, um die Anforderungen der Anwendung zu erfüllen.  | | ✓ | ✓ | 284 |
| **1.4.3** | Überprüfen Sie die Durchsetzung des Prinzips der wenigsten erforderlichen Privilegien (_least privilege_) bei Funktionen, Dateien, URLs, Controllern, Diensten und anderen Ressourcen. Dies impliziert den Schutz vor Spoofing und die Erweiterung von Privilegien. |  | ✓ | ✓ | 272 |
| **1.4.4** | Vergewissern Sie sich, dass die Kommunikation zwischen Anwendungskomponenten, einschließlich APIs, Middleware und Datenschichten, mit den am wenigsten erforderlichen Berechtigungen (_least privilege_) durchgeführt wird.
 ([C3](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 272 |
| **1.4.5** | Überprüfen Sie, dass die Anwendung einen einzigen und gut erprobten Zugriffskontrollmechanismus für den Zugriff auf geschützte Daten und Ressourcen verwendet. Alle Anfragen müssen diesen einzigen Mechanismus durchlaufen, um Kopieren und Einfügen oder unsichere Alternativpfade zu vermeiden.
 ([C7](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) |  | ✓ | ✓ | 284 |
| **1.4.6** | Stellen Sie sicher, dass eine attribut- oder merkmalsbasierte Zugriffskontrolle verwendet wird, wobei der Code die Berechtigung des Benutzers für ein Merkmal/Datenelement und nicht nur seine Rolle prüft. Die Berechtigungen sollten weiterhin über Rollen zugewiesen werden.
 ([C7](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 275 |

## V1.5 Anforderungen an die Eingabe- und Ausgabe-Architektur

In Version 4.0 haben wir uns von dem Begriff _server-seitig_ als etablierte Vertrauensgrenze verabschiedet. Die Vertrauensgrenze ist immer noch ein Thema - Entscheidungen über nicht vertrauenswürdige Browser oder Client-Geräte zu treffen, können weiterhin umgangen werden. In den heutigen Standardarchitekturen hat sich jedoch der Punkt der Vertrauensdurchsetzung (_Trust Enforcement_) dramatisch verändert. Wenn in dem ASVS der Begriff _vertrauenswürdige Serviceschicht_ verwendet wird, meinen wir daher jeden vertrauenswürdigen Durchsetzungspunkt, unabhängig vom Standort, wie z.B. einen Microservice, eine _serverless_ API, eine serverseitige, eine vertrauenswürdige API auf einem Clientgerät, usw.

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.5.1** | Vergewissern Sie sich, dass die Eingabe- und Ausgabeanforderungen klar definieren, wie die Daten auf der Grundlage des Typs, des Inhalts und der anwendbaren Gesetze, Vorschriften und anderen Richtlinien zu behandeln und zu verarbeiten sind.
  | | ✓ | ✓ | 1029 |
| **1.5.2** | Stellen Sie sicher, dass bei der Kommunikation mit nicht vertrauenswürdigen Clients keine Serialisierung verwendet wird. Wenn dies nicht möglich ist, stellen Sie sicher, dass angemessene Integritätskontrollen (und möglicherweise Verschlüsselung, wenn sensible Daten gesendet werden) durchgesetzt werden, um Deserialisierungsangriffe einschließlich der Injektion von Objekten zu verhindern. | | ✓ | ✓ | 502 |
| **1.5.3** | Vergewissern Sie sich, dass die Eingabevalidierung auf einer vertrauenswürdigen Serviceschicht durchgesetzt wird. ([C5](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 602 |
| **1.5.4** | Vergewissern Sie sich, dass die Ausgabekodierung in der Nähe des oder durch den Interpreter erfolgt, für den sie bestimmt ist. ([C4](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 116 |

## V1.6 Anforderungen an die kryptographische Architektur

Anwendungen müssen mit einer Architektur für eine starke Kryptographie entworfen werden, um die Datenbestände gemäß ihrer Klassifizierung zu schützen. Alles zu verschlüsseln ist verschwenderisch, nichts zu verschlüsseln ist rechtlich fahrlässig. Es muss ein Gleichgewicht gefunden werden, in der Regel während des Architektur- oder High-Level-Designs, bei Design-Sprints oder Architektur-Spikes. Wenn Sie die Kryptographie nach und nach entwerfen oder nachrüsten, wird die sichere Implementierung unweigerlich viel mehr kosten, als wenn Sie sie gleich von Anfang an einbauen würden.

Architektonische Anforderungen sind der gesamten Codebasis inhärent und daher schwierig zu vereinheitlichen oder zu integrieren. Die architektonischen Anforderungen müssen bei den Kodierungsstandards während der gesamten Umsetzungsphase berücksichtigt werden und sollten während der Sicherheitsarchitektur, bei Peer- oder Code-Reviews oder bei Retrospektiven überprüft werden.

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.6.1** | Vergewissern Sie sich, dass es eine explizite Richtlinie für die Verwaltung von kryptografischen Schlüsseln gibt und dass der Lebenszyklus eines kryptografischen Schlüssels einem Schlüsselverwaltungsstandard wie NIST SP 800-57 folgt. | | ✓ | ✓ | 320 |
| **1.6.2** | Stellen Sie sicher, dass Verwender von kryptografischen Diensten Schlüsselmaterial und andere Geheimnisse schützen, indem Sie Key Vaults oder API-basierte Alternativen verwenden. | | ✓ | ✓ | 320 |
| **1.6.3** | Vergewissern Sie sich, dass alle Schlüssel und Passwörter austauschbar sind und Teil eines genau definierten Prozesses zur Neuverschlüsselung sensibler Daten sind. | | ✓ | ✓ | 320 |
| **1.6.4** | Vergewissern Sie sich, dass symmetrische Schlüssel, Kennwörter oder API-Geheimnisse, die von Kunden erzeugt oder mit ihnen geteilt werden, nur zum Schutz von Geheimnissen mit geringem Risiko, wie z.B. die Verschlüsselung des lokalen Speichers, oder für vorübergehende, kurzzeitige Verwendungen wie die Verschleierung von Parametern, verwendet werden. Das Teilen von Geheimnissen mit Kunden ist gleichzusetzen mit dem Teilen von Klartext und sollte auch architektonisch als solches behandelt werden.
 | | ✓ | ✓ | 320 |

## V1.7 Architektonische Anforderungen an Fehlerbehandlung, Protokollierung und Auditierung

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.7.1** | Vergewissern Sie sich, dass im gesamten System ein einheitliches Protokollformat und ein einheitlicher Protokollierungsansatz verwendet wird.  ([C9](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 1009 |
| **1.7.2** | Vergewissern Sie sich, dass die Protokolle sicher an ein, vorzugsweise entferntes, System zur Analyse, Erkennung, Alarmierung und Eskalation übertragen werden.
 ([C9](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | |

## V1.8 Architektonische Anforderungen für Datenschutz und Privatsphäre

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.8.1** | Vergewissern Sie sich, dass alle sensiblen Daten identifiziert und in Schutzstufen eingeteilt werden. | | ✓ | ✓ | |
| **1.8.2** | Vergewissern Sie sich, dass alle Schutzebenen mit einer Reihe von Schutzanforderungen verbunden sind, z.B. Verschlüsselungsanforderungen, Integritätsanforderungen, Aufbewahrung, Datenschutz und andere Vertraulichkeitsanforderungen, und dass diese in der Architektur angewendet werden. | | ✓ | ✓ | |

## V1.9 Architektonische Anforderungen an die Kommunikation

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.9.1** | Überprüfen Sie, ob die Anwendung die Kommunikation zwischen Komponenten verschlüsselt, insbesondere wenn sich diese Komponenten in verschiedenen Containern, Systemen, Standorten oder Cloud-Anbietern befinden. ([C3](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 319 |
| **1.9.2** | Überprüfen Sie, dass die Anwendungskomponenten die Authentizität jeder Seite in einer Kommunikationsverbindung überprüfen, um "Person-in-the-Middle"-Angriffe zu verhindern. Beispielsweise sollten Anwendungskomponenten TLS-Zertifikate und -Ketten validieren. |  | ✓ | ✓ | 295 |

## V1.10 Architekturanforderungen hinsichtlich bösartiger Software

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.10.1** | Vergewissern Sie sich, dass ein Quellcode-Kontrollsystem verwendet wird, mit Verfahren, die sicherstellen, dass beim Einchecken zugehörige Tickets referenziert werden. Das Quellcode-Kontrollsystem sollte über eine Zugriffskontrolle und identifizierbare Benutzer verfügen, um die Rückverfolgbarkeit von Änderungen zu ermöglichen. | | ✓ | ✓ | 284 |

## V1.11 Architekturanforderungen an die Geschäftslogik

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.11.1** | Überprüfen Sie die Definition und Dokumentation aller Anwendungskomponenten in Bezug auf die von ihnen bereitgestellten Geschäfts- oder Sicherheitsfunktionen. | | ✓ | ✓ | 1059 |
| **1.11.2** | Vergewissern Sie sich, dass alle kritischen Abläufe der Geschäftslogik, einschließlich Authentifizierung, Sitzungsverwaltung und Zugriffskontrolle, keinen unsynchronisierten Zustand aufweisen. | | ✓ | ✓ | 362 |
| **1.11.3** | Vergewissern Sie sich, dass alle kritischen Abläufe der Geschäftslogik, einschließlich Authentifizierung, Sitzungsverwaltung und Zugriffskontrolle, thread-sicher und resistent gegen Prüfzeit- und Nutzungszeit-Nebenläufigkeiten sind. | | | ✓ | 367 |

## V1.12 Architekturanforderungen an sicheres Hochladen von Dateien

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.12.1** | Überprüfen Sie, ob die vom Benutzer hochgeladenen Dateien außerhalb des Web-Stammverzeichnisses gespeichert sind. | | ✓ | ✓ | 552 |
| **1.12.2** | Vergewissern Sie sich, dass die vom Benutzer hochgeladenen Dateien - falls sie angezeigt oder von der Anwendung heruntergeladen werden müssen - entweder durch Octet-Stream-Downloads oder von einer nicht verwandten Domäne, wie z.B. einem Cloud File Storage Bucket, bereitgestellt werden. Implementieren Sie eine geeignete Content Security Policy (CSP), um das Risiko von XSS-Vektoren oder anderen Angriffen auf die hochgeladene Datei zu reduzieren. | | ✓ | ✓ | 646 |

## V1.13 Architekturanforderungen für APIs

Dies dient als Platzhalter für zukünftige Architekturanforderungen.

## V1.14 Architekturanforderungen für die Konfiguration

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **1.14.1** | Überprüfen Sie die Verwendung eindeutiger oder spezieller Betriebssystemkonten mit niedriger Privilegierung für alle Anwendungskomponenten, Dienste und Server.
 ([C3](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 250 |
| **1.14.2** | Überprüfen Sie die Trennung von Komponenten unterschiedlicher Vertrauensebenen durch klar definierte Sicherheitskontrollen, Firewall-Regeln, API-Gateways, Reverse-Proxies, Cloud-basierte Sicherheitsgruppen oder vergleichbare Mechanismen.
 | | ✓ | ✓ | 923 |
| **1.14.3** | Stellen Sie sicher, dass bei der Bereitstellung von Binärdateien auf nicht vertrauenswürdigen Geräten binäre Signaturen, vertrauenswürdige Verbindungen und verifizierte Endpunkte verwendet werden. | | ✓ | ✓ | 494 |
| **1.14.4** | Vergewissern Sie sich, dass die Build-Pipeline vor veralteten oder unsicheren Komponenten warnt und entsprechende Maßnahmen ergreift.
 | | ✓ | ✓ | 1104 |
| **1.14.5** | Vergewissern Sie sich, dass die Build-Pipeline einen Build-Schritt enthält, um die sichere Bereitstellung der Anwendung automatisch zu erstellen und zu verifizieren, insbesondere wenn es sich bei der Anwendungsinfrastruktur um Software handelt, wie z.B. Build-Skripts für Cloud-Umgebungen. | | ✓ | ✓ | |
| **1.14.6** | Vergewissern Sie sich, dass Anwendungsimplementierungen auf der Netzwerkebene angemessen sandboxed, containerisiert und/oder isoliert sind, um Angriffe zu verzögern und Angreifer davon abzuhalten, andere Anwendungen anzugreifen, insbesondere wenn sie sensible oder gefährliche Aktionen wie Deserialisierung durchführen. ([C5](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 265 |
| **1.14.7** | Stellen Sie sicher, dass die Anwendung keine nicht mehr unterstützte, unsicheren oder veralteten clientseitigen Technologien wie NSAPI-Plugins, Flash, Shockwave, ActiveX, Silverlight, NACL oder clientseitige Java-Applets verwendet. | | ✓ | ✓ | 477 |

## Referenzen

Für weitere Informationen siehe auch:

* [OWASP Threat Modeling Cheat Sheet](https://www.owasp.org/index.php/Threat_Modeling_Cheat_Sheet)
* [OWASP Attack Surface Analysis Cheat Sheet](https://www.owasp.org/index.php/Attack_Surface_Analysis_Cheat_Sheet)
* [OWASP Threat modeling](https://www.owasp.org/index.php/Application_Threat_Modeling)
* [OWASP Secure SDLC Cheat Sheet](https://www.owasp.org/index.php/Secure_SDLC_Cheat_Sheet)
* [Microsoft SDL](https://www.microsoft.com/en-us/sdl/)
* [NIST SP 800-57](https://csrc.nist.gov/publications/detail/sp/800-57-part-1/rev-4/final)
