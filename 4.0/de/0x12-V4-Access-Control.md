# V4: Anforderungen für die Überprüfung der Zugriffskontrolle

## Zielsetzung

Autorisierung ist das Konzept, den Zugang zu den Ressourcen nur denjenigen zu gestatten, die diese auch verwenden dürfen. Stellen Sie sicher, dass eine überprüfte Anwendung die folgenden High-Level Anforderungen erfüllt:

* Personen, die auf Ressourcen zugreifen, verfügen über gültige Anmeldedaten hierfür.
* Benutzer sind mit einem klar definierten Satz von Rollen und Privilegien verknüpft.
* Metadaten für Rollen und Berechtigungen sind vor Replay-Attacken oder Manipulation geschützt.

## Anforderungen an die Sicherheitsüberprüfung

## V4.1 Allgemeine Entwurfsrichtlinien für die Zugriffskontrolle

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **4.1.1** | Vergewissern Sie sich, dass die Anwendung Zugriffskontrollregeln auf einer vertrauenswürdigen Dienstschicht durchsetzt, insbesondere wenn die Zugriffskontrolle auf der Client-Seite vorhanden ist und umgangen werden könnte. | ✓ | ✓ | ✓ | 602 |
| **4.1.2** | Vergewissern Sie sich, dass alle Benutzer- und Datenattribute und Richtlinieninformationen, die von den Zugriffskontrollen verwendet werden, von den Endbenutzern nicht manipuliert werden können, es sei denn, dies wird ausdrücklich genehmigt. | ✓ | ✓ | ✓ | 639 |
| **4.1.3** | Überprüfen Sie, ob das Prinzip der geringstmöglichen Privilegien (_least privilege_) angewandt wird - Benutzer sollten nur auf Funktionen, Dateien, URLs, Controller, Dienste und andere Ressourcen zugreifen können, für die sie eine bestimmte Berechtigung besitzen. Dies impliziert einen Schutz gegen Spoofing und gegen eine Erhöhung der Privilegien. ([C7](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ |  285 |
| **4.1.4** | Vergewissern Sie sich, dass das Prinzip der standardmäßigen Verweigerung (_deny by default_) besteht, wonach neue Benutzer/Rollen mit minimalen oder gar keinen Berechtigungen starten und Benutzer/Rollen keinen Zugang zu neuen Funktionen erhalten, bis der Zugang explizit zugewiesen wird.  ([C7](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ |  276 |
| **4.1.5** | Vergewissern Sie sich, dass die Zugriffskontrollen Anfragen entsprechend sicher ablehnen, auch wenn eine Ausnahme auftritt. ([C10](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ |  285 |

## V4.2 Zugriffskontrolle auf Betriebsebene

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **4.2.1** | Vergewissern Sie sich, dass sensible Daten und APIs vor direkten Objektangriffen geschützt sind, die auf das Erstellen, Lesen, Aktualisieren und Löschen von Datensätzen abzielen, z.B. das Erstellen oder Aktualisieren von Datensätzen einer anderen Person, das Anzeigen aller Datensätze oder das Löschen aller Datensätze. | ✓ | ✓ | ✓ | 639 |
| **4.2.2** | Vergewissern Sie sich, dass die Anwendung oder das verwendete Framework einen starken Anti-CSRF-Mechanismus zum Schutz authentifizierter Funktionalität durchsetzt und dass eine effektive Anti-Automatisierung oder Anti-CSRF nicht authentifizierte Funktionalität schützt. | ✓ | ✓ | ✓ | 352 |

## V4.3 Weitere Überlegungen zur Zugangskontrolle

| # | Beschreibung | L1 | L2 | L3 | CWE |
| :---: | :--- | :---: | :---:| :---: | :---: |
| **4.3.1** | Überprüfen Sie, ob die administrativen Schnittstellen eine geeignete Multi-Faktor-Authentifizierung verwenden, um eine unbefugte Nutzung zu verhindern. | ✓ | ✓ | ✓ | 419 |
| **4.3.2** | Vergewissern Sie sich, dass die Navigation in Verzeichnissen deaktiviert ist, es sei denn, dies ist absichtlich erwünscht. Außerdem sollten Anwendungen das Auffinden oder die Offenlegung von Datei- oder Verzeichnis-Metadaten, wie z.B. _Thumbs.db_, _.DS_Store_, _.git_ oder _.svn_ Ordner, nicht zulassen. | ✓ | ✓ | ✓ | 548 |
| **4.3.3** | Vergewissern Sie sich, dass die Anwendung über zusätzliche Berechtigungen (wie z.B. ansteigende oder adaptive Authentifizierung) für Systeme mit geringerem Wert und/oder eine Aufgabentrennung für kritische Anwendungen mit hohem Wert verfügt, um Betrugsbekämpfungskontrollen entsprechend dem Risiko der Anwendung und früherer Betrugsfälle durchzusetzen. |  | ✓ | ✓ |  732 |

## Verweise

Für weitere Informationen siehe auch:

* [OWASP Testing Guide 4.0: Authorization](https://www.owasp.org/index.php/Testing_for_Authorization)
* [OWASP Cheat Sheet: Access Control](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Access_Control_Cheat_Sheet.md)
* [OWASP CSRF Cheat Sheet](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.md)
* [OWASP REST Cheat Sheet](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/REST_Security_Cheat_Sheet.md)
