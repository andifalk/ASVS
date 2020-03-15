# V2: Anforderungen für die Prüfung der Authentifizierung

## Zielsetzung

Authentifizierung ist der Akt der Feststellung oder Bestätigung, dass jemand (oder etwas) glaubwürdig ist und dass die von einer Person oder über ein Gerät gemachten Behauptungen korrekt sind, widerstandsfähig gegen Nachahmung sind und die Wiederherstellung oder das Abfangen von Passwörtern verhindern.

Als der ASVS zum ersten Mal veröffentlicht wurde, war außerhalb von Hochsicherheitssystemen die Kombination aus Benutzername + Passwort die gebräuchlichste Form der Authentifizierung. Die Multi-Faktor-Authentifizierung (MFA) war zwar in Sicherheitskreisen allgemein akzeptiert, aber wurde anderswo nur selten verlangt. Seit die Zahl der Passwortverletzungen zunahm, machte der Gedanke, dass Benutzernamen irgendwie vertraulich und Passwörter unbekannt sind, viele Sicherheitskontrollen untragbar. So betrachtet beispielsweise NIST 800-63 die Benutzernamen und wissensbasierte Authentifizierung (KBA) als öffentliche Information, SMS- und E-Mail-Benachrichtigungen als [_eingeschränkte_ Authentifizierungstypen](https://pages.nist.gov/800-63-FAQ/#q-b1) und Passwörter als potentiell verletzt. Diese Realität macht wissensbasierte Authentifikatoren, SMS- und E-Mail-Wiederherstellung, Passwortverläufe, Komplexität und Rotationskontrollen nutzlos. Diese Kontrollen waren schon immer wenig hilfreich und zwangen die Benutzer dazu, sich alle paar Monate neue schwache Passwörter auszudenken, aber mit der Veröffentlichung von über 5 Milliarden Verletzungen von Benutzernamen und Passwörtern ist es an der Zeit, weiter voranzuschreiten.

Von allen Abschnitten innerhalb des ASVS haben sich die Kapitel Authentifizierung und Sitzungsverwaltung am häufigsten verändert. Die Einführung einer führenden effektiven, wissenschaftlich fundierten Praxis wird für viele eine Herausforderung sein, und das ist völlig in Ordnung. Wir müssen jetzt mit dem Übergang zu einer _Post-Passwort_ Zukunft starten.

## NIST 800-63 - Ein moderner, wissenschaftlich fundierter Authentifizierungsstandard

[NIST 800-63b](https://pages.nist.gov/800-63-3/sp800-63b.html) ist ein moderner, wissenschaftlich fundierter Standard und stellt unabhängig von dessen Anwendbarkeit die beste aktuell verfügbare Empfehlung dar. Der Standard ist für alle Organisationen auf der ganzen Welt hilfreich, aber besonders relevant für US-Behörden und diejenigen, die mit US-Behörden zu tun haben.

Die Terminologie nach NIST 800-63 kann anfangs etwas verwirrend sein, besonders wenn man nur die Authentifizierung per Benutzername und Passwort gewohnt ist. Fortschritte in der modernen Authentifizierung sind notwendig, daher müssen wir eine Terminologie einführen, die in Zukunft allgemein üblich sein wird. Aber wir können auch die Verständnisschwierigkeiten nachvollziehen bis sich die ganze Branche auf diese neuen Begrifflichkeiten eingestellt hat. Wir haben zur Unterstützung am Ende dieses Kapitels ein Glossar bereitgestellt. Wir haben viele Anforderungen umformuliert, um dem Zweck der Anforderung zu entsprechen und nich nur der Absichtserklärung zu dienen. Zum Beispiel verwendet der ASVS den Begriff _Passwort_, obwohl das NIST in diesem Standard _memorized secret_ als Begriff verwendet.

ASVS V2-Authentifizierung, V3-Sitzungsmanagement und in geringerem Maße auch V4-Zugangskontrollen wurden so angepasst, dass sie eine übereinstimmende Teilmenge ausgewählter NIST 800-63b-Kontrollen darstellen, die sich auf allgemeine Bedrohungen und häufig ausgenutzte Authentifizierungsschwächen konzentrieren. Wenn eine vollständige Konformität zu NIST 800-63 erforderlich ist, dann ziehen Sie bitte das Dokument zu NIST 800-63 zu Rate.

### Auswahl einer geeigneten NIST AAL-Stufe

Der Application Security Verification Standard hat versucht, die ASVS Stufe 1 den NIST AAL1-Anforderungen, die Stufe 2 den AAL2-Anforderungen und die Stufe 3 den AAL3-Anforderungen zuzuordnen. Der Ansatz der ASVS-Stufe 1 als "wesentliche" Kontrollen ist jedoch nicht unbedingt die richtige AAL-Stufe zur Prüfung einer Anwendung oder API. Wenn es sich bei der Anwendung beispielsweise um eine Anwendung der Stufe 3 handelt oder wenn die Anwendung die gesetzlichen Anforderungen an AAL3 erfüllt, sollte in den Abschnitten V2 und V3 Session Management die Stufe 3 gewählt werden. Die Wahl der NIST-konformen Authentifizierungs-Assertion-Level (AAL) sollte gemäß den Richtlinien von NIST 800-63b erfolgen, wie in *Selecting AAL* in [NIST 800-63b Abschnitt 6.2](https://pages.nist.gov/800-63-3/sp800-63-3.html#AAL_CYOA) festgelegt.

## Die Erklärung dazu

Applications can always exceed the current level's requirements, especially if modern authentication is on an application's roadmap. Previously, the ASVS has required mandatory MFA. NIST does not require mandatory MFA. Therefore, we have used an optional designation in this chapter to indicate where the ASVS encourages but does not require a control. The following keys are used throughout this standard:

Anwendungen können immer die Anforderungen der aktuellen Stufe überschreiten, insbesondere wenn eine moderne Authentifizierung auf der Roadmap der Anwendung steht. Früher hat der ASVS obligatorisch eine MFA verlangt. Das NIST verlangt keine obligatorische MFA. Daher haben wir in diesem Kapitel eine optionale Bezeichnung verwendet, um anzugeben, wo der ASVS eine Kontrolle empfiehlt, aber nicht verlangt. Die folgenden Schlüssel werden in diesem Standard verwendet:

| Kennzeichnung | Beschreibung |
| :--: | :-- |
| | Nicht erforderlich |
| o | Empfohlen, aber nicht erforderlich |
| ✓ | Erforderlich |

## V2.1 Anforderungen an die Passwortsicherheit

Passwörter, die von NIST 800-63 als _Memorized Secrets_ bezeichnet werden, umfassen Passwörter, PINs, Entsperrmuster, die Auswahl des richtigen Kätzchens oder eines anderen Bildelements sowie Passphrasen. Sie werden im Allgemeinen als "etwas, das Sie kennen" betrachtet und oft als Ein-Faktor-Authentifikatoren verwendet. Die weitere Verwendung der Ein-Faktor-Authentifizierung ist mit erheblichen Herausforderungen verbunden. Dazu gehören Milliarden von gültigen Kombinationen aus Benutzernamen und Passwörtern, die im Internet offengelegt werden, Standardpasswörter oder schwache Passwörter, _Rainbow Tables_ und Wörterbücher der gängigsten Passwörter.

Die Anwendungen sollten die Benutzer nachdrücklich dazu auffordern, sich für die Multi-Faktor-Authentifizierung anzumelden, und sollten es den Benutzern ermöglichen, Token wiederzuverwenden, die sie bereits besitzen, wie z.B. FIDO- oder U2F-Token, oder sich mit einem Identityprovider zu verbinden, der Multi-Faktor-Authentifizierung anbietet.

Identityprovider (__C__redential __s__ervice __p__roviders, CSPs) bieten eine föderierte Identität für Benutzer an. Benutzer verfügen oft über mehr als eine Identität mit mehreren CSPs, z.B. eine Unternehmensidentität mit _Azure AD_, _Okta_, _Ping Identity_ sowie _Google_ oder eine Social-Media-Identität mit _Facebook_, _Twitter_, _Google_ oder _WeChat_, um nur einige gängige Alternativen zu nennen. Diese Liste ist keine Empfehlung dieser Unternehmen oder Dienste, sondern lediglich eine Ermutigung für Entwickler, die Realität zu berücksichtigen, dass viele Benutzer mehrere etablierte Identitäten haben. Organisationen sollten entsprechend dem Risikoprofil bezüglich der Stärke der Identitätsprüfung durch den CSP die Integration mit bestehenden Benutzeridentitäten in Betracht ziehen. So ist es beispielsweise unwahrscheinlich, dass eine Regierungsorganisation eine Social-Media-Identität als Login für sensible Systeme akzeptiert, da es einfach möglich ist, gefälschte oder _Wegwerf-Identitäten_ zu erstellen, während ein Unternehmen für Handyspiele möglicherweise eine Integration mit großen Social-Media-Plattformen vornehmen muss, um seine aktive Spielerbasis zu vergrößern.

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **2.1.1** | Vergewissern Sie sich, dass die Passwörter der Benutzer mindestens 12 Zeichen lang sind. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.2** | Stellen Sie sicher, dass Passwörter mit mindestens 64 Zeichen erlaubt sind. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.3** | Stellen Sie sicher, dass Passwörter Leerzeichen enthalten können und dass kein Abschneiden von Zeichen durchgeführt wird. Mehrere aufeinander folgende Leerzeichen KÖNNEN optional zusammengeführt werden. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.4** | Überprüfen Sie, ob Unicode-Zeichen in Kennwörtern zulässig sind. Ein einzelner Unicode-Codepoint wird als Zeichen betrachtet, daher sollten 12 Emoji- oder 64 Kanji-Zeichen gültig und erlaubt sein. | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.5** | Stellen Sie sicher, dass Benutzer ihr Passwort ändern können. | ✓ | ✓ | ✓ | 620 | 5.1.1.2 |
| **2.1.6** | Vergewissern Sie sich, dass die Funktionalität zur Kennwortänderung das aktuelle und das neue Kennwort des Benutzers erfordert. | ✓ | ✓ | ✓ | 620 | 5.1.1.2 |
| **2.1.7** | Vergewissern Sie sich, dass die bei der Konto-Registrierung, Anmeldung und Passwortänderung übermittelten Passwörter entweder lokal (z.B. die 1.000 oder 10.000 häufigsten Passwörter, die mit der Passwortrichtlinie des Systems übereinstimmen) oder mit Hilfe einer externen API gegen einen Satz von verletzten Passwörtern geprüft werden. Bei Verwendung einer API sollte ein Nachweis über die Unkenntnis oder ein anderer Mechanismus verwendet werden, um sicherzustellen, dass das Klartext-Passwort nicht gesendet oder zur Überprüfung des Verletzungsstatus des Passworts verwendet wird. Wenn das Passwort verletzt wird, muss die Anwendung den Benutzer auffordern, ein neues, nicht verletztes Passwort zu setzen. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.8** | Vergewissern Sie sich, dass eine Anzeige zur Passwort-Stärke zur Verfügung gestellt wird, um Benutzern die Einstellung eines stärkeren Passworts zu erleichtern. | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.9** | Stellen Sie sicher, dass es keine Regeln für Zusammensetzung des Passworts gibt, die die Art der zulässigen Zeichen einschränken. Es sollte keine Groß- oder Kleinschreibung, Zahlen oder Sonderzeichen vorgeschrieben werden. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.10** | Vergewissern Sie sich, dass es keine Anforderungen an die periodischen Rotation der Anmeldedaten oder die Kennworthistorie gibt. | ✓ | ✓ | ✓ | 263 | 5.1.1.2 |
| **2.1.11** | Stellen Sie sicher, dass die _Paste_-Funktionalität, Browser-Passworthilfen und externe Passwortmanager zugelassen sind. | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |
| **2.1.12** | Prüfen Sie, dass der Benutzer auf Plattformen, die dies nicht als native Funktionalität haben, wählen kann, entweder vorübergehend das gesamte maskierte Kennwort anzuzeigen oder vorübergehend das letzte eingetippte Zeichen des Kennworts anzuzeigen. | ✓ | ✓ | ✓ | 521 | 5.1.1.2 |

Note: The goal of allowing the user to view their password or see the last character temporarily is to improve the usability of credential entry, particularly around the use of longer passwords, passphrases, and password managers. Another reason for including the requirement is to deter or prevent test reports unnecessarily requiring organizations to override native platform password field behavior to remove this modern user-friendly security experience.

__Hinweis__: Das Ziel, dem Benutzer die Möglichkeit zu geben, sein Passwort einzusehen oder vorübergehend das letzte Zeichen zu sehen, ist es, die Benutzerfreundlichkeit bei der Eingabe von Anmeldeinformationen zu verbessern, insbesondere bei der Verwendung längerer Passwörter, Passphrasen und Passwort-Manager. Ein weiterer Grund für die Aufnahme der Anforderung ist das Verhindern von Testberichten, welche Organisationen unnötigerweise dazu zwingen, das native Verhalten der Plattform für Passwortfelder zu überschreiben, um diese moderne benutzerfreundliche Sicherheitserfahrung zu entfernen.

## V2.2 Allgemeine Anforderungen an den Authentifizierer

Die Agilität des Authentisierers ist für zukunftssichere Anwendungen unerlässlich. Refactorings der Authentisierers sind notwendig, um zusätzliche Authentifikatoren gemäß den Benutzerpräferenzen zuzulassen und um veraltete oder unsichere Authentifikatoren in geordneter Weise aus dem Verkehr zu ziehen.

Das NIST betrachtet E-Mail und SMS als [_eingeschränkte_ Authentifizierertypen](https://pages.nist.gov/800-63-FAQ/#q-b1), und es ist wahrscheinlich, dass sie irgendwann in der Zukunft aus dem NIST 800-63 und damit dem ASVS entfernt werden. Anwendungen sollten in ihrer Roadmap eine Authentifizierung einplanen, die keine Verwendung von E-Mail oder SMS erfordert.

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **2.2.1** | Prüfen Sie, dass Anti-Automatisierungskontrollen wirksam sind, wenn es darum geht, Angriffe auf verletze Anmeldedaten, Brute Forcing und Kontosperren zu minimieren. Zu diesen Kontrollen gehören u.a. das Blockieren der am häufigsten gebrochenen Passwörter, Soft-Lockouts, Rate Limiting, CAPTCHA, zunehmende Verzögerungen zwischen den Anmeldeversuchen, IP-Adressbeschränkungen oder risikobasierte Einschränkungen bezüglich des Standorts, der erste Anmeldung auf einem Gerät, der letzten Versuche, das Konto zu entsperren. Stellen Sie sicher, dass nicht mehr als 100 Fehlversuche pro Stunde bei einem einzelnen Konto möglich sind. | ✓ | ✓ | ✓ | 307 | 5.2.2 / 5.1.1.2 / 5.1.4.2 / 5.1.5.2 |
| **2.2.2** | Prüfen Sie, dass der Einsatz schwacher Authentifikatoren (wie SMS und E-Mail) auf die sekundäre Verifizierung und Genehmigung der Transaktion beschränkt ist und nicht als Ersatz für sicherere Authentifizierungsmethoden dient. Vergewissern Sie sich, dass stärkere Methoden angeboten werden, bevor schwache Methoden eingesetzt werden, dass sich die Benutzer der Risiken bewusst sind, oder dass geeignete Maßnahmen zur Begrenzung der Risiken einer Kontoverletzung getroffen werden. | ✓ | ✓ | ✓ | 304 | 5.2.10 |
| **2.2.3** | Vergewissern Sie sich, dass nach Aktualisierungen der Authentifizierungsdetails, wie z.B. das Zurücksetzen von Anmeldedaten, E-Mail- oder Adressänderungen, Anmeldungen aus unbekannten oder risikoreichen Standorten, Sicherheitsbenachrichtigungen an Benutzer gesendet werden. Die Verwendung von Push-Benachrichtigungen - anstelle von SMS oder E-Mail - ist vorzuziehen, aber bei Fehlen von Push-Benachrichtigungen sind SMS oder E-Mail akzeptabel, solange in der Benachrichtigung keine sensiblen Informationen offengelegt werden. | ✓ | ✓ | ✓ | 620 | |
| **2.2.4** | Überprüfen Sie die Widerstandsfähigkeit gegen Phishing, z.B. durch die Verwendung von Multi-Faktor-Authentifizierung, kryptografische Geräte mit Bestätigung (z.B. Online-Schlüssel mit einer Push-Möglichkeit zur Authentifizierung) oder auf höheren AAL-Ebenen clientseitige Zertifikate. |  |  | ✓ | 308 | 5.2.5 |
| **2.2.5** | Stellen Sie sicher, dass dort, wo ein Identity Provider (CSP) und die Anwendung, die die Authentifizierung verifiziert, getrennt sind, Mutual TLS zwischen den beiden Endpunkten vorhanden ist. |  |  | ✓ | 319 | 5.2.6 |
| **2.2.6** | Überprüfen Sie die Widerstandsfähigkeit gegenüber Replayangriffen durch den vorgeschriebenen Einsatz von OTP-Geräten, kryptografischen Authentifikatoren oder Backupcodes. |  |  | ✓ | 308 | 5.2.8 |
| **2.2.7** | Verifizieren Sie die Absicht, sich zu authentifizieren, indem Sie die Eingabe eines OTP-Tokens oder eine vom Benutzer initiierte Aktion, wie z.B. einen Tastendruck auf einem FIDO-Hardwareschlüssel, verlangen. |  |  | ✓ | 308 | 5.2.9 |

## V2.3 Anforderungen an den Lebenszyklus des Authentisierers

Als Authentisierer dienen Passwörter, Soft-Token, Hardware-Token und biometrische Geräte. Der Lebenszyklus von Authentifikatoren ist für die Sicherheit einer Anwendung entscheidend - wenn jemand ein Konto ohne Identitätsnachweis selbst registrieren kann, kann es kaum Vertrauen in die Identitätsprüfung geben. Für Social-Media-Sites wie Reddit ist das völlig in Ordnung. Bei Banksystemen ist ein stärkerer Fokus auf die Registrierung und Ausgabe von Anmeldedaten und Geräten für die Sicherheit der Anwendung entscheidend.

__Hinweis__: Passwörter dürfen keine maximale Lebensdauer haben oder einer Passwort-Rotation unterliegen. Passwörter sollten stattdessen auf eine Verletzung überprüft und nicht regelmäßig ersetzt werden.

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **2.3.1** | Die vom System generierten Initialpasswörter oder Aktivierungscodes MÜSSEN sicher zufällig generiert werden, mindestens 6 Zeichen lang sein und KÖNNEN Buchstaben und Zahlen enthalten und sollten nach einer kurzen Zeitspanne ablaufen. Diese initialen Anmeldedaten dürfen nicht zum Langzeit-Passwort werden. | ✓ | ✓ | ✓ | 330 | 5.1.1.2 / A.3 |
| **2.3.2** | Vergewissern Sie sich, dass die Registrierung und die Verwendung der vom Teilnehmer bereitgestellten Authentifizierungsgeräte unterstützt werden, wie z.B. U2F- oder FIDO-Token. |  | ✓ | ✓ | 308 | 6.1.3 |
| **2.3.3** | Vergewissern Sie sich, dass die Anweisungen zur Erneuerung mit genügend Zeitvorlauf gesendet werden, um zeitgebundene Authentifizierer erneuern zu können. |  | ✓ | ✓ | 287 | 6.1.4 |

## V2.4 Anforderungen für die Speicherung von Anmeldedaten

This section cannot be penetration tested, so controls are not marked as L1. However, this section is of vital importance to the security of credentials if they are stolen, so if forking the ASVS for an architecture or coding guideline or source code review checklist, please place these controls back to L1 in your private version.

Architekten und Entwickler sollten sich bei der Erstellung oder dem Refactoring von Code an die Ausführungen dieses Kapitels halten. Dieser Teil kann nur durch Quellcodeüberprüfung oder durch sichere Unit- oder Integrationstests vollständig überprüft werden. Penetrationstests können keines dieser Probleme identifizieren.

Die Liste der genehmigten _One-way Key Derivation Functions_ ist in NIST 800-63 B Abschnitt 5.1.1.2 und in [BSI Kryptographische Verfahren: Empfehlungen und Schlussell&auml;ngen (2018)](https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Publikationen/TechnischeRichtlinien/TR02102/BSI-TR-02102.pdf?__blob=publicationFile) ausführlich beschrieben. Anstelle dieser Auswahlmöglichkeiten können die neuesten nationalen oder regionalen Algorithmen und Schlüssellängenstandards gewählt werden.

Dieser Abschnitt kann nicht mittels Penetrationstests geprüft werden, daher sind die Kontrollen nicht mit der Stufe 1 gekennzeichnet. Dieser Abschnitt ist jedoch von entscheidender Bedeutung für die Sicherheit von Anmeldedaten, für den Fall, dass diese gestohlen werden. Wenn Sie einen Fork des ASVSs für eine Architektur- oder Kodierungsrichtlinie oder eine Checkliste zur Überprüfung des Quellcodes erstellt haben, platzieren Sie diese Kontrollen bitte in Ihrer eigenen Version zurück auf Stufe 1.

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **2.4.1** | Vergewissern Sie sich, dass die Passwörter in einer Form gespeichert sind, die gegen Offline-Angriffe resistent ist. Passwörter MÜSSEN gesalzen (_salted_) und unter Verwendung einer anerkannten Einweg-Schlüsselableitung (_One-way Key Derivation_)  oder einer Passwort-Hashing-Funktion gehasht werden. Die Funktionen zur Einweg-Schlüsselableitung und zum Passwort-Hashing nehmen zur Generierung eines Passwort-Hashes ein Passwort, einen Salt und einen Kostenfaktor als Eingabe. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 916 | 5.1.1.2 |
| **2.4.2** | Vergewissern Sie sich, dass das Salt mindestens 32 Bit lang ist, und wählen Sie es willkürlich, um Salzwertkollisionen zwischen gespeicherten Hashes zu minimieren. Für jedes Credential MUSS ein eindeutiger Salzwert und der daraus resultierende Hash gespeichert werden. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 916 | 5.1.1.2 |
| **2.4.3** | Vergewissern Sie sich, dass bei Verwendung von _PBKDF2_ die Iterationszahl so groß sein SOLLTE, wie es die Leistung des Verifikationsservers zulässt, normalerweise mindestens 100.000 Iterationen. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 916 | 5.1.1.2 |
| **2.4.4** | Vergewissern Sie sich, dass bei Verwendung von _bcrypt_ der Arbeitsfaktor so groß sein SOLLTE, wie es die Leistung des Verifikationsservers erlaubt, normalerweise mindestens 13. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | | ✓ | ✓ | 916 | 5.1.1.2 |
| **2.4.5** | Vergewissern Sie sich, dass eine zusätzliche Iteration einer  Schlüsselableitung durchgeführt wird, wobei ein Salzwert verwendet wird, der geheim und nur dem Verifizierer bekannt ist. Generieren Sie den Salzwert mit einem zugelassenen Zufallsbitgenerator [_SP 800-90Ar1_] und stellen Sie mindestens die in der letzten Revision von _SP 800-131A_ angegebene Mindestsicherheitsstärke bereit. Der geheime Saltwert MUSS getrennt von den gehashten Passwörtern gespeichert werden (z.B. in einem speziellen Gerät wie einem Hardware-Sicherheitsmodul). |  | ✓ | ✓ | 916 | 5.1.1.2 |

Dort wo US-Normen erwähnt werden, kann je nach Bedarf eine regionale oder lokale Norm anstelle der US-Norm oder zusätzlich zu dieser verwendet werden.

## V2.5 Anforderungen für die Wiederherstellung von Anmeldedaten

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **2.5.1** | Stellen Sie sicher, dass ein vom System generiertes Geheimnis zur Erstaktivierung oder Wiederherstellung nicht im Klartext an den Benutzer gesendet wird. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 640 | 5.1.1.2 |
| **2.5.2** | Stellen Sie sicher, dass keine Hinweise auf Passwörter oder wissensbasierte Authentifizierung (so genannte _Sicherheitsfragen_) vorhanden sind. | ✓ | ✓ | ✓ | 640 | 5.1.1.2 |
| **2.5.3** | Stellen Sie sicher, dass die Wiederherstellung von Kennwortdaten das aktuelle Kennwort in keiner Weise Preis gibt. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 640 | 5.1.1.2 |
| **2.5.4** | Überprüfen Sie, dass gemeinsame Konten oder Standardkonten nicht vorhanden sind (z.B. _root_, _admin_ oder _sa_). | ✓ | ✓ | ✓ | 16 | 5.1.1.2 / A.3 |
| **2.5.5** | Vergewissern Sie sich, dass der Benutzer darüber informiert wird, wenn ein Authentifizierungsfaktor geändert oder ersetzt wird. | ✓ | ✓ | ✓ | 304 | 6.1.2.3 |
| **2.5.6** | Stellen Sie sicher, dass Sie für vergessene Kennwörter und andere Wiederherstellungspfade einen sicheren Wiederherstellungsmechanismus verwenden, wie z.B. TOTP oder andere Soft-Token, Mobile Push bzw. einen anderen Offline-Wiederherstellungsmechanismus. ([C6](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=Formal_Numbering)) | ✓ | ✓ | ✓ | 640 | 5.1.1.2 |
| **2.5.7** | Vergewissern Sie sich, dass bei Verlust von OTP- oder Multi-Faktor-Authentifizierungsfaktoren der Identitätsnachweis auf der gleichen Ebene wie bei der Registrierung durchgeführt wird. |  | ✓ | ✓ | 308 | 6.1.2.3 |

## V2.6 Anforderungen für Nachschlagelisten von Sicherheitscodes

Geheimnisse aus Nachschlagewerken sind vorgenerierte Listen von Geheimcodes, ähnlich wie Transaktionsberechtigungsnummern (TAN), Wiederherstellungscodes für soziale Medien oder ein Raster, das eine Reihe von Zufallswerten enthält. Diese werden sicher an die Benutzer verteilt. Diese Nachschlagecodes werden einmal verwendet, und wenn alle verwendet werden, wird die Nachschlageliste verworfen. Diese Art von Authentifizierer wird als "etwas, das Sie haben" betrachtet.

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **2.6.1** | Stellen Sie sicher, dass Geheimnisse aus Nachschlagewerken nur einmal verwendet werden können.
 |  | ✓ | ✓ | 308 | 5.1.2.2 |
| **2.6.2** | Vergewissern Sie sich, dass die Geheimnisse aus Nachschlagewerken eine ausreichende Zufälligkeit aufweisen (112 Bit Entropie) oder, falls weniger als 112 Bit Entropie vorhanden sind, mit einem einzigartigen und zufälligen 32-Bit-Salz gesalzen und mit einem anerkannten Einweghash gehasht werden.
 |  | ✓ | ✓ | 330 | 5.1.2.2 |
| **2.6.3** | Vergewissern Sie sich, dass Geheimnisse aus Nachschlagewerken gegen Offline-Angriffe, wie z.B. vorhersehbare Werte, resistent sind.
 |  | ✓ | ✓ | 310 | 5.1.2.2 |

## V2.7 Anforderungen für Sicherheitsinformationen auf einem zweiten Kanal

In der Vergangenheit wäre eine übliche Prüfung auf einem zweiten Kanal eine E-Mail oder SMS mit einem Link zum Zurücksetzen des Passworts gewesen. Angreifer nutzen aber diesen schwachen Mechanismus, um Konten, die sie noch nicht kontrollieren, zurückzusetzen, z.B. indem sie das E-Mail-Konto einer Person übernehmen und entdeckte Reset-Links wieder verwenden. Es gibt bessere Möglichkeiten, die Verifizierung auf einem zweiten Kanal zu handhaben.

Sichere Sekundärkanal-Authentifikatoren sind physische Geräte, die mit dem Verifizierer über einen sicheren Sekundärkanal kommunizieren können. Beispiele hierfür sind Push-Benachrichtigungen an mobile Geräte. Diese Art von Authentifizierern wird als "etwas, das Sie haben" betrachtet. Wenn ein Benutzer sich authentifizieren möchte, sendet die verifizierende Anwendung eine Nachricht an den Sekundärkanal-Authentifikator über eine Verbindung direkt zum Authentifikator oder indirekt über einen Drittanbieterdienst. Die Nachricht enthält einen Authentifizierungscode (typischerweise eine zufällige sechsstellige Zahl oder einen modalen Genehmigungsdialog). Die verifizierende Anwendung wartet auf den Empfang des Authentifizierungscodes über den Primärkanal und vergleicht den Hash des empfangenen Wertes mit dem Hash des ursprünglichen Authentifizierungscodes. Wenn sie übereinstimmen, kann der Verifizierer des Sekundärkanals davon ausgehen, dass der Benutzer sich authentifiziert hat.

Der ASVS geht davon aus, dass nur wenige Entwickler neue Sekundärkanal-Authentifizierer wie Push-Benachrichtigungen entwickeln werden, und daher gelten die folgenden ASVS-Steuerelemente für Verifizierer, wie z.B. Authentifizierungs-API, Anwendungen und Single-Sign-On-Implementierungen. Wenn Sie einen neuen Sekundärkanal-Authentifikator entwickeln, lesen Sie bitte NIST 800-63B &sect; 5.1.3.1.

Unsichere Sekundärkanal-Authentifizierer wie E-Mail und VOIP sind nicht zulässig. PSTN- und SMS-Authentifizierung sind derzeit durch NIST _eingeschränkt_ und sollten zugunsten von Push-Benachrichtigungen oder ähnlichem eingestellt werden. Wenn Sie Telefon- oder SMS-Sekundärkanal-Authentifizierung verwenden müssen, lesen Sie bitte &sect; 5.1.3.3.

| # | Beschreibung | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **2.7.1** | Vergewissern Sie sich, dass Klartext-Sekundärkanal-Authentifikatoren (NIST _restricted_), wie z.B. SMS oder PSTN, nicht standardmäßig angeboten werden, und dass zunächst stärkere Alternativen wie Push-Benachrichtigungen angeboten werden.

 | ✓ | ✓ | ✓ | 287 | 5.1.3.2 |
| **2.7.2** | Vergewissern Sie sich, dass der Sekundärkanal-Überprüfer Authentifizierungsanforderungen, -Codes oder -Token nach 10 Minuten invalidiert.
 | ✓ | ✓ | ✓ | 287 | 5.1.3.2 |
| **2.7.3** | Vergewissern Sie sich, dass Authentifizierungsanfragen, -Codes oder -Token des Sekundärkanal-Überprüfers nur einmal und nur für die ursprüngliche Authentifizierungsanfrage verwendbar sind.
 | ✓ | ✓ | ✓ | 287 | 5.1.3.2 |
| **2.7.4** | Überprüfen Sie, ob der Sekundärkanal-Authentifizierer und der Verifizierer über einen sicheren, unabhängigen Kanal kommunizieren. | ✓ | ✓ | ✓ | 523 | 5.1.3.2 |
| **2.7.5** | Stellen Sie sicher, dass der Sekundärkanal-Überprüfer nur eine gehashte Version des Authentifizierungscodes aufbewahrt. |  | ✓ | ✓ | 256 | 5.1.3.2 |
| **2.7.6** | Vergewissern Sie sich, dass der anfängliche Authentifizierungscode von einem sicheren Zufallszahlengenerator erzeugt wird, der mindestens 20 Bit Entropie enthält (normalerweise ist eine sechsfache digitale Zufallszahl ausreichend).

 |  | ✓ | ✓ | 310 | 5.1.3.2 |

## V2.8 Anforderungen an eine Ein- oder Mehrfaktor-Prüfung

Einmalpasswörter mit einem Faktor (OTP) sind physische oder Soft Token, die eine sich ständig ändernde pseudo-zufällige _one time challenge_ darstellen. Diese Geräte machen Phishing (Nachahmung) schwierig, aber nicht unmöglich. Diese Art von Authentifikatoren wird als "etwas, das Sie haben" betrachtet. Multi-Faktor-Token sind ähnlich wie Ein-Faktor-OTPs, erfordern jedoch einen gültigen PIN-Code, biometrische Entsperrung, USB-Anschluss oder NFC-Paarung oder einen zusätzlichen Wert (z.B. einen Transaktionssignierungsrechner), der eingegeben werden muss, um den endgültigen OTP zu erstellen.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **2.8.1** | Verify that time-based OTPs have a defined lifetime before expiring. | ✓ | ✓ | ✓ | 613 | 5.1.4.2 / 5.1.5.2 |
| **2.8.2** | Verify that symmetric keys used to verify submitted OTPs are highly protected, such as by using a hardware security module or secure operating system based key storage. |  | ✓ | ✓ | 320 | 5.1.4.2 / 5.1.5.2|
| **2.8.3** | Verify that approved cryptographic algorithms are used in the generation, seeding, and verification. |  | ✓ | ✓ | 326 | 5.1.4.2 / 5.1.5.2 |
| **2.8.4** | Verify that time-based OTP can be used only once within the validity period. |  | ✓ | ✓ | 287 | 5.1.4.2 / 5.1.5.2 |
| **2.8.5** | Verify that if a time-based multi factor OTP token is re-used during the validity period, it is logged and rejected with secure notifications being sent to the holder of the device. |  | ✓ | ✓ | 287 | 5.1.5.2 |
| **2.8.6** | Verify physical single factor OTP generator can be revoked in case of theft or other loss. Ensure that revocation is immediately effective across logged in sessions, regardless of location. |  | ✓ | ✓ | 613 | 5.2.1 |
| **2.8.7** | Verify that biometric authenticators are limited to use only as secondary factors in conjunction with either something you have and something you know. |  | o | ✓ | 308 | 5.2.3 |

## V2.9 Cryptographic Software and Devices Verifier Requirements

Cryptographic security keys are smart cards or FIDO keys, where the user has to plug in or pair the cryptographic device to the computer to complete authentication. Verifiers send a challenge nonce to the cryptographic devices or software, and the device or software calculates a response based upon a securely stored cryptographic key.

The requirements for single factor cryptographic devices and software, and multi-factor cryptographic devices and software are the same, as verification of the cryptographic authenticator proves possession of the authentication factor.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **2.9.1** | Verify that cryptographic keys used in verification are stored securely and protected against disclosure, such as using a TPM or HSM, or an OS service that can use this secure storage. |  | ✓ | ✓ | 320 | 5.1.7.2 |
| **2.9.2** | Verify that the challenge nonce is at least 64 bits in length, and statistically unique or unique over the lifetime of the cryptographic device. |  | ✓ | ✓ | 330 | 5.1.7.2 |
| **2.9.3** | Verify that approved cryptographic algorithms are used in the generation, seeding, and verification. | | ✓ | ✓ | 327 | 5.1.7.2 |

## V2.10 Service Authentication Requirements

This section is not penetration testable, so does not have any L1 requirements. However, if used in an architecture, coding or secure code review, please assume that software (just as Java Key Store) is the minimum requirement at L1. Clear text storage of secrets is not acceptable under any circumstances.

| # | Description | L1 | L2 | L3 | CWE | [NIST &sect;](https://pages.nist.gov/800-63-3/sp800-63b.html) |
| :---: | :--- | :---: | :---:| :---: | :---: | :---: |
| **2.10.1** | Verify that integration secrets do not rely on unchanging passwords, such as API keys or shared privileged accounts. |  | OS assisted | HSM | 287 | 5.1.1.1 |
| **2.10.2** | Verify that if passwords are required, the credentials are not a default account. |  | OS assisted | HSM | 255 | 5.1.1.1 |
| **2.10.3** | Verify that passwords are stored with sufficient protection to prevent offline recovery attacks, including local system access. |  | OS assisted | HSM | 522 | 5.1.1.1 |
| **2.10.4** | Verify passwords, integrations with databases and third-party systems, seeds and internal secrets, and API keys are managed securely and not included in the source code or stored within source code repositories. Such storage SHOULD resist offline attacks. The use of a secure software key store (L1), hardware trusted platform module (TPM), or a hardware security module (L3) is recommended for password storage. |  | OS assisted | HSM | 798 | |

## Additional US Agency Requirements

US Agencies have mandatory requirements concerning NIST 800-63. The Application Security Verification Standard has always been about the 80% of controls that apply to nearly 100% of apps, and not the last 20% of advanced controls or those that have limited applicability. As such, the ASVS is a strict subset of NIST 800-63, especially for IAL1/2 and AAL1/2 classifications, but is not sufficiently comprehensive, particularly concerning IAL3/AAL3 classifications.

We strongly urge US government agencies to review and implement NIST 800-63 in its entirety.

## Glossary of terms

| Term | Meaning |
| -- | -- |
| CSP | Credential Service Provider also called an Identity Provider |
| Authenticator | Code that authenticates a password, token, MFA, federated assertion, and so on. |
| Verifier | "An entity that verifies the claimant's identity by verifying the claimant's possession and control of one or two authenticators using an authentication protocol. To do this, the verifier may also need to validate credentials that link the authenticator(s) to the subscriber's identifier and check their status" |
| OTP | One-time password |
| SFA | Single factor authenticators, such as something you know (memorized secrets, passwords, passphrases, PINs), something you are (biometrics, fingerprint, face scans), or something you have (OTP tokens, a cryptographic device such as a smart card),  |
| MFA | Multi factor authenticator, which includes two or more single factors |

## References

For more information, see also:

* [NIST 800-63 - Digital Identity Guidelines](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63-3.pdf)
* [NIST 800-63 A - Enrollment and Identity Proofing](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63a.pdf)
* [NIST 800-63 B - Authentication and Lifecycle Management](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63b.pdf)
* [NIST 800-63 C - Federation and Assertions](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63c.pdf)
* [NIST 800-63 FAQ](https://pages.nist.gov/800-63-FAQ/)
* [OWASP Testing Guide 4.0: Testing for Authentication](https://www.owasp.org/index.php/Testing_for_authentication)
* [OWASP Cheat Sheet - Password storage](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Password_Storage_Cheat_Sheet.md)
* [OWASP Cheat Sheet - Forgot password](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Forgot_Password_Cheat_Sheet.md)
* [OWASP Cheat Sheet - Choosing and using security questions](https://www.owasp.org/index.php/Choosing_and_Using_Security_Questions_Cheat_Sheet)
