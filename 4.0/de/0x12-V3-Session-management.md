# V3: Anforderungen an die Sitzungsmanagementprüfung

## Zielsetzung

Eine der Kernkomponenten jeder webbasierten Anwendung oder zustandsabhängigen API ist ein Mechanismus, mit dessen Hilfe sie den Zustand für einen Benutzer oder ein Gerät, das mit ihr interagiert, steuert und aufrechterhält. Die Sitzungsverwaltung transformiert ein zustandsloses Protokoll in ein zustandsbehaftetes, was für die Unterscheidung verschiedener Benutzer oder Geräte entscheidend ist.

Es muss sichergestellt werden, dass eine geprüfte Anwendung die folgenden High-Level Anforderungen an das Sitzungsmanagement erfüllt:

* Sitzungen sind für jede Person einzigartig und können nicht erraten oder geteilt werden.
* Sitzungen werden als ungültig gekennzeichnet, wenn sie nicht mehr benötigt werden, und werden während inaktiver Phasen zeitweise deaktiviert.

Wie bereits erwähnt, wurden diese Anforderungen so angepasst, dass sie eine konforme Teilmenge ausgewählter NIST 800-63b-Kontrollen darstellen, die sich auf gemeinsame Bedrohungen und häufig ausgenutzte Authentifizierungsschwächen konzentrieren. Frühere Prüfungsanforderungen wurden zurückgezogen, abgeschafft oder in vielen Fällen so angepasst, dass sie sich stark an den Zielen der obligatorischen Anforderungen [NIST 800-63b](https://pages.nist.gov/800-63-3/sp800-63b.html) orientieren.

## Anforderungen an die Sicherheitsüberprüfung

## V3.1 Grundlegende Anforderungen an das Sitzungsmanagement

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **3.1.1** | Vergewissern Sie sich, dass die Anwendung niemals Session-Tokens in URL-Parametern oder Fehlermeldungen offenlegt.  | ✓ | ✓ | ✓ | 598 |  |

## V3.2 Anforderungen an die Sitzungsbindung

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **3.2.1** | Überprüfen Sie, ob die Anwendung bei jeder Benutzerauthentifizierung immer ein neues Sitzungs-Token erzeugt. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 384 | 7.1 |
| **3.2.2** | Überprüfen Sie, ob Sitzungs-Token mindestens 64 Bit Entropie aufweisen. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 331 | 7.1 |
| **3.2.3** | Vergewissern Sie sich, dass die Anwendung Sitzungs-Token im Browser nur mit sicheren Methoden wie z.B. entsprechend gesicherten Cookies (siehe Abschnitt 3.4) oder mit Hilfe von HTML 5 Session Storage speichert. | ✓ | ✓ | ✓ | 539 | 7.1 |
| **3.2.4** | Vergewissern Sie sich, dass die Sitzungs-Token mit anerkannten kryptografischen Algorithmen generiert werden. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 331 | 7.1 |

TLS oder ein anderer entsprechend sicherer Transportkanal ist für die Sitzungsverwaltung obligatorisch. Dies wird im Kapitel Kommunikationssicherheit behandelt.

## V3.3 Anforderungen für Sitzungsabmeldung und -timeouts

Die Session-Timeouts wurden an NIST 800-63 angeglichen, der wesentlich längere Session-Timeouts erlaubt, als die Sicherheitsstandards traditionell erlauben. Unternehmen sollten die nachstehende Tabelle überprüfen, und wenn ein längeres Timeout aufgrund des Risikos der Anwendung wünschenswert ist, sollte der NIST-Wert die obere Grenze der Session-Timeouts im Leerlauf sein.

Stufe 1 entspricht in diesem Zusammenhang IAL1/AAL1, Stufe 2 entspricht IAL2/AAL3, Stufe 3 entspricht IAL3/AAL3. Für IAL2/AAL2 und IAL3/AAL3 ist das kürzere Timeout die untere Grenze der Leerlaufzeit für die Abmeldung oder erneute Authentifizierung zur Wiederaufnahme der Sitzung.

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **3.3.1** | Vergewissern Sie sich, dass die Abmeldung und der Ablauf der Sitzung das Sitzungs-Token ungültig machen, so dass der Zurück-Button oder eine sonstige nachgeschaltete vertrauenswürdige Partei eine authentifizierte Sitzung nicht wieder aufnimmt, auch nicht zwischen den Vertrauensparteien. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 613 | 7.1 |
| **3.3.2** | Wenn Authentifizierer den Benutzern erlauben, angemeldet zu bleiben, überprüfen Sie, dass eine erneute Authentifizierung in regelmäßigen Abständen sowohl bei aktiver Nutzung als auch nach einer Leerlaufphase erfolgt. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | 30 Tage | 12 Stunden oder 30 Minuten der Inaktivität, 2FA Optional | 12 Stunden oder 15 Minuten der Inaktivität, mit 2FA | 613 | 7.2 |
| **3.3.3** | Vergewissern Sie sich, dass die Anwendung alle anderen aktiven Sitzungen nach einer erfolgreichen Kennwortänderung beendet, und dass dies in der gesamten Anwendung, der föderierten Anmeldung (falls vorhanden) und in allen sich darauf vertrauenden Parteien wirksam ist. |  | ✓ | ✓ | 613 | |
| **3.3.4** | Überprüfen Sie, ob die Benutzer in der Lage sind, vereinzelte oder alle derzeit aktiven Sitzungen und Geräte anzuzeigen und sich davon abzumelden. |  | ✓ | ✓ | 613 | 7.1 |

## V3.4 Cookie-basierte Sitzungsverwaltung

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **3.4.1** | Vergewissern Sie sich, dass Cookie-basierte Session-Tokens das Attribut _Secure_ gesetzt haben. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 614 | 7.1.1 |
| **3.4.2** | Überprüfen Sie, dass Cookie-basierte Session-Tokens das Attribut _HttpOnly_ gesetzt haben. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 1004 | 7.1.1 |
| **3.4.3** | Verifizieren Sie, dass Cookie-basierte Session-Tokens das _SameSite_ Attribut verwenden, um die Anfälligkeit für Cross-Site Request Forgery (CSRF) Angriffe zu begrenzen. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 16 | 7.1.1 |
| **3.4.4** | Stellen Sie sicher, dass Cookie-basierte Session-Tokens den Präfix ___Host-_ verwenden (siehe Referenzen), um die Vertraulichkeit von Session-Cookies zu gewährleisten. | ✓ | ✓ | ✓ | 16 | 7.1.1 |
| **3.4.5** | Wenn die Anwendung unter einem gemeinsamen Domänennamen zusammen mit anderen Anwendungen veröffentlicht wird, die Sitzungscookies setzen oder verwenden, welche die Sitzungscookies außer Kraft setzen oder offenlegen könnten, stellen Sie das Pfadattribut in Cookie-basierten Sitzungs-Tokens unter Verwendung des konkretesten Pfades ein. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 16 | 7.1.1 |

## V3.5 Token-basierte Sitzungsverwaltung

Die tokenbasierte Sitzungsverwaltung umfasst JWT-, OAuth-, SAML- und API-Schlüssel. Von diesen sind die API-Schlüssel bekanntermaßen schwach und sollten in neu implementiertem Code nicht verwendet werden.

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **3.5.1** | Vergewissern Sie sich, dass die Anwendung OAuth und Refresh Tokens nicht &mdash; selbst bearbeitet &mdash; als die Anwesenheit eines Teilnehmers auffasst und es so den Benutzern ermöglicht, Vertrauensbeziehungen mit verknüpften Anwendungen zu beenden.  |  | ✓ | ✓ | 290 | 7.1.2 |
| **3.5.2** | Überprüfen Sie, dass die Anwendung Sitzungs-Tokens anstelle von statischen API-Geheimnissen und -Schlüsseln verwendet, außer bei Legacy-Implementierungen. |  | ✓ | ✓ | 798 | |
| **3.5.3** | Verifizieren Sie, dass zustandslose Session-Tokens digitale Signaturen, Verschlüsselung und andere Gegenmaßnahmen zum Schutz gegen Angriffe wie Manipulation, Verschleierung, Replay, Null-Chiffren und Schlüsselaustausch verwenden. |  | ✓ | ✓ | 345 | |

## V3.6 Erneute Authentifizierung einer Föderation oder anderweitigen Erklärung

Dieser Abschnitt bezieht sich auf diejenigen, die den Code für die vertrauenswürdigen Partei (_Relying Party_, RP) oder den Code für den _Credential Service Provider_ (CSP) schreiben. Wenn Sie sich auf Code verlassen, der diese Funktionen implementiert, stellen Sie sicher, dass die nachfolgenden Probleme korrekt behandelt werden.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **3.6.1** | Vergewissern Sie sich, dass die vertrauenswürdigen Parteien die maximale Authentifizierungszeit gegenüber den _Credential Service Providers_ (CSPs) angeben und dass die CSPs den Teilnehmer erneut authentifizieren, wenn sie innerhalb dieses Zeitraums keine Sitzung genutzt haben. | | | ✓ | 613 | 7.2.1 |
| **3.6.2** | Vergewissern Sie sich, dass die _Credential Service Provider_ (CSPs) die vertrauenswürdigen Parteien (_Relying Party_, RP) über das letzte Authentifizierungsereignis informieren, damit die RPs feststellen können, ob sie den Benutzer erneut authentifizieren müssen. | | | ✓ | 613| 7.2.1 |

## V3.7 Schutz vor Ausnutzung von Schwächen des Sitzungsmanagements

Es gibt eine kleine Anzahl von Angriffen auf das Sitzungsmanagement, von denen einige mit der User Experience (UX) von Sitzungen zusammenhängen. Zuvor hat der ASVS auf der Grundlage der Anforderungen der ISO 27002 das Blockieren mehrerer gleichzeitiger Sitzungen gefordert. Das Blockieren gleichzeitiger Sitzungen ist nicht mehr angemessen, nicht nur, weil heutige Benutzer viele Geräte haben oder die Anwendung eine API ohne Browser-Sitzung ist. In den meisten dieser Implementierungen gewinnt der letzte Authentifizierer, der oft der Angreifer ist. Dieser Abschnitt bietet eine weiterführende Anleitung zum Abhalten, Verzögern und Erkennen von Angriffen auf das Sitzungsmanagement mittels Programmcode.

### _Half-Open_ Angriffe

Anfang 2018 wurden mehrere Finanzinstitutionen durch so genannte _Half-Open_ Angriffe kompromittiert. Dieser Begriff ist in der Branche hängen geblieben. Die Angreifer schlugen bei mehreren Institutes mit unterschiedlichen proprietären Code-Basen zu, und in der Tat scheint es verschiedene Code-Basen innerhalb derselben Institute zu geben. Der _Half-Open_ Angriff nutzt einen Designfehler aus, der in vielen bestehenden Authentifizierungs-, Sitzungsverwaltungs- und Zugangskontrollsystemen zu finden ist.

Die Angreifer beginnen einen _Half-Open_ Angriff, indem sie versuchen, ein Anmeldedatum zu sperren, zurückzusetzen oder wiederherzustellen. Ein beliebtes Design-Pattern für die Sitzungsverwaltung setzt auf die Wiederverwendung von Sitzungsobjekten und -modellen des Benutzerprofils zwischen nicht authentifiziertem, halb-authentifiziertem (Kennwortrücksetzung, vergessener Benutzername) und vollständig authentifiziertem Code. Dieses Entwurfsmuster befüllt ein gültiges Sitzungsobjekt oder Token mit dem Profil des Opfers, einschließlich Passwort-Hashes und Rollen. Wenn die Zugriffskontrollprüfungen in Controllern oder Routern nicht korrekt überprüfen, ob ein Benutzer vollständig angemeldet ist, kann der Angreifer im Namen dieses Benutzers handeln.  
Angriffe könnten u.a. die Änderung des Benutzerkennworts auf einen bekannten Wert, die Aktualisierung der E-Mail-Adresse zur Durchführung einer gültigen Kennwortrücksetzung, die Deaktivierung der Multi-Faktor-Authentifizierung oder die Registrierung eines neuen MFA-Geräts oder die Offenlegung bzw. Änderung von API-Schlüsseln umfassen.

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **3.7.1** | Vergewissern Sie sich, dass die Anwendung eine gültige Anmeldesitzung gewährleistet oder eine erneute Authentifizierung oder sekundäre Überprüfung erfordert, bevor sensible Transaktionen oder Kontoänderungen zugelassen werden. | ✓ | ✓ | ✓ | 778 | |

## Verweise

Für weitere Informationen siehe auch:

* [OWASP Testing Guide 4.0: Session Management Testing](https://www.owasp.org/index.php/Testing_for_Session_Management)
* [OWASP Session Management Cheat Sheet](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Session_Management_Cheat_Sheet.md)
* [Set-Cookie __Host- prefix details](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie#Directives)
