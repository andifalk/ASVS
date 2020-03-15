# Prüfung und Zertifizierung

## Die Haltung der OWASP zu ASVS-Zertifizierungen und Vertrauenssiegeln

OWASP als herstellerneutrale, gemeinnützige Organisation zertifiziert derzeit keine Anbieter, Verifizierer oder Software für ASVS.

Alle derartigen Zusicherungen, Vertrauenssiegel oder Zertifizierungen werden von OWASP nicht offiziell überprüft, registriert oder zertifiziert, so dass eine Organisation, die sich auf eine solche Prüfung verlässt, vorsichtig sein muss, was das Vertrauen in eine dritte Partei oder ein Vertrauenssiegel betrifft, das eine ASVS-Zertifizierung für sich beansprucht.

Dies sollte aber Organisationen auch nicht daran hindern, derartige Dienstleistungen anzubieten, solange sie keine offizielle OWASP-Zertifizierung beanspruchen.

## Leitfaden für zertifizierende Organisationen

Der Application Security Verification Standard kann für volltransparente Prüfungen von Anwendungen verwendet werden, einschließlich des offenen und ungehinderten Zugangs zu Schlüsselressourcen wie Architekten und Entwickler, Projektdokumentation, Quellcode, authentifizierter Zugang zu Testsystemen (inklusive des Zugangs zu Konten in jeder Rolle), insbesondere für Verifikationen der Stufen 2 und 3.

In der Vergangenheit haben Penetrationstests und Überprüfungen von sicherem Code ausnahmslos Probleme beinhaltet - das heißt, dass nur fehlgeschlagene Tests im Abschlussbericht erscheinen. Eine zertifizierende Organisation muss in jedem Bericht folgende Angaben mit aufnehmen:

* Den Umfang der Verifizierung (insbesondere, wenn eine Schlüsselkomponente außerhalb des Umfangs liegt, wie z.B. die SSO-Authentifizierung)
* Eine Zusammenfassung der Verifizierungsergebnisse, einschließlich der bestandenen und nicht bestandenen Tests, mit klaren Angaben zur Lösung der fehlgeschlagenen Tests.

Bestimmte Prüfungsanforderungen sind möglicherweise nicht auf die zu prüfende Anwendung anwendbar. Wenn Sie beispielsweise Ihren Kunden eine zustandslose Service-Schicht API ohne eine zugehörige Client-Implementierung zur Verfügung stellen, sind viele der Anforderungen in _V3 Session Management_ nicht direkt anwendbar. In solchen Fällen kann eine zertifizierende Organisation immer noch die volle ASVS-Konformität beanspruchen, muss aber in jedem Bericht klar einen Grund für die Nichtanwendbarkeit solcher ausgeschlossener Prüfungsanforderungen angeben.

Die Aufbewahrung von detaillierten Arbeitsaufzeichnungen, Screenshots oder Videos, Skripts zur verlässlichen und wiederholten Ausnutzung eines Problems und elektronischen Aufzeichnungen von Tests, wie z.B. das Abfangen von Proxy-Protokollen und zugehörigen Notizen, wie z.B. einer Bereinigungsliste, gilt als Industriestandard und kann für die kritischsten Entwickler als Beweis für die Ergebnisse nützlich sein. Es reicht nicht aus, einfach ein Tool laufen zu lassen und über die Fehler zu berichten; dies liefert (überhaupt) keinen ausreichenden Beweis dafür, dass alle Probleme auf einer Zertifizierungsebene gründlich getestet und geprüft worden sind. Im Falle von Streitigkeiten sollte es genügend Sicherheitsbeweise geben, um nachzuweisen, dass jede einzelne verifizierte Anforderung tatsächlich auch getestet wurde.

### Testmethoden

Zertifizierende Organisationen können die geeignete(n) Prüfmethode(n) frei wählen, sollten diese jedoch in einem Bericht aufführen.

Je nach der zu prüfenden Anwendung und den Prüfungsanforderungen können unterschiedliche Prüfmethoden verwendet werden, um ein hinreichendes Vertrauen in die Ergebnisse zu gewinnen. Die Überprüfung der Wirksamkeit von Eingabevalidierungsmechanismen einer Anwendung kann beispielsweise entweder mittels eines manuellen Penetrationstests oder mit Hilfe von Quellcodeanalysen durchgeführt werden.

#### Die Rolle automatisierter Sicherheitswerkzeuge

Der Einsatz von Werkzeugen für automatisierte Penetrationstests wird empfohlen, um eine möglichst hohe Testabdeckung zu erreichen.

Es ist nicht möglich, die vollständige ASVS-Prüfung nur mit automatisierten Penetrationstesttools alleine abzudecken. Während eine große Anzahl der Anforderungen in Stufe 1 mit automatisierten Tests überprüft werden kann, ist die überwiegende Mehrheit der Anforderungen nicht für automatisierte Penetrationstests geeignet.

Bitte beachten Sie, dass die Grenzen zwischen automatisierten und manuellen Tests mit zunehmender Reife in der Anwendungssicherheitsindustrie immer mehr verschwimmen. Automatisierte Werkzeuge werden häufig von Experten manuell optimiert, und manuelle Tester nutzen oft eine Vielzahl automatisierter Werkzeuge.

#### Die Rolle von Penetrationstests

In Version 4.0 haben wir uns entschieden, die Stufe 1 vollständig penetrationstestbar zu machen, ohne Zugriff auf Quellcode, Dokumentation oder Entwickler zu erfordern. Zwei Protokollierungselemente, die zur Einhaltung der OWASP Top 10 2017 A10 erforderlich sind, erfordern Interviews, Screenshots oder eine andere Sammlung von Beweisen, wie sie auch in der OWASP Top 10 2017 erforderlich sind. Das Testen ohne Zugang zu den notwendigen Informationen ist jedoch keine ideale Methode der Sicherheitsüberprüfung, da die Möglichkeit versäumt wird, ein Code-Review zu etablieren, Bedrohungen und fehlende Kontrollen zu identifizieren und einen weitaus gründlicheren Test in kürzerer Zeit durchzuführen.

Wenn möglich, ist bei der Durchführung einer Bewertung nach den Stufen 2 oder 3 der Zugang zu Entwicklern, Dokumentation, Code und Zugriff auf eine Testanwendung mit nicht produktiven Daten erforderlich. Penetrationstests, die auf diesen Ebenen durchgeführt werden, erfordern diese Zugriffsebene, die wir als _Hybride Überprüfungen_ oder _Hybride Penetrationstests_ nennen.

## Andere Verwendungszwecke des ASVS

Abgesehen von der Verwendung zur Bewertung der Sicherheit einer Anwendung haben wir eine Reihe anderer möglicher Anwendungen für den ASVS identifiziert.

### Detaillierter Leitfaden für eine Sicherheitsarchitektur

Eine der häufigeren Anwendungen des Application Security Verification Standards ist die Verwendung als Ressource für Sicherheitsarchitekten. In der _Sherwood Applied Business Security Architecture (SABSA)_ fehlt eine Vielzahl an Informationen, die für eine gründliche Überprüfung einer sicheren Anwendungsarchitektur erforderlich sind. ASVS kann verwendet werden, um diese Lücken zu füllen, indem Sicherheitsarchitekten bessere Kontrollen für häufige Probleme, wie z.B. Best Practices für Datenschutz und Strategien für Eingabevalidierung, wählen können.

### Als Ersatz für Standard Secure Coding Checklisten

Viele Organisationen können von der Übernahme des ASVS profitieren, indem sie sich für eine der drei Stufen entscheiden oder einen _Fork_ des ASVS erstellen und die Anforderungen für jede Anwendungsrisikostufe domänenspezifisch ändern. Wir fördern diese Art der Abzweigung, solange die Rückverfolgbarkeit gewährleistet ist. Das heisst, wenn eine Anwendung die Anforderung 4.1 bestanden hat, soll dies für die Verzweigung dasselbe bedeuten wie für den sich weiter entwickelnde Standard.

### Als Leitfaden für automatisierte Unit- und Integrationstests

Der ASVS ist so konzipiert, dass er in hohem Maße testbar ist - mit der einzigen Ausnahme der Anforderungen an die Architektur und Vermeidung bösartigen Codes. Durch die Erstellung von Unit- und Integrationstests, die auf spezifische und relevante Fuzzing- und Missbrauchsfälle testen, wird die Anwendung mit jedem einzelnen Build nahezu _selbstverifizierend_. Beispielsweise können zusätzliche Tests für die Testsuite eines Login-Controllers erstellt werden, die den Benutzernamen auf gebräuchliche Standardbenutzernamen, _Account Enumeration_, _Brute-Forcing_, LDAP- und SQL-Injektionen und XSS-Angriffe testen. In ähnlicher Weise sollte ein Test für das Kennwort übliche Standard-Kennwörter, Kennwortlänge, Null-Byte-Injektionen, Entfernen des Kennwortparameters, XSS und mehr umfassen.

### Für Trainings zur sicheren Entwicklung

Der ASVS kann auch dazu verwendet werden, Merkmale sicherer Software zu definieren. Viele Trainingskurse zur "sicheren Kodierung" sind einfach ethische Hacking-Kurse mit nur einem kurzen Ausflug zu _Secure Coding_. Dies hilft den Entwicklern aber nicht unbedingt, sichereren Code zu schreiben. Stattdessen können sichere Entwicklungskurse den ASVS verwenden, wobei der Schwerpunkt hier auf den _ProActive Controls_ des ASVS liegt und nicht auf den OWASP Top 10 der Fehler, die man nicht machen sollte.

### Als Treiber für die Sicherheit agil entwickelter Anwendungen

Der ASVS kann innerhalb eines agilen Entwicklungsprozesses als Rahmenwerk verwendet werden, um spezifische Aufgaben z.B. innerhalb eines Sprints zu definieren, die vom Team implementiert werden müssen, um ein sicheres Produkt zu erhalten. Ein Ansatz könnte sein: Beginnen Sie mit Stufe 1, prüfen Sie ihre Anwendung oder das System gemäß den ASVS-Anforderungen für die spezifizierte Stufe, finden Sie heraus, welche Kontrollen fehlen und erfassen Sie spezifische Tickets/Aufgaben im Backlog. Dies hilft bei der Priorisierung bestimmter Aufgaben (z.B. beim Grooming/Refinement) und macht die Sicherheit im agilen Prozess sichtbar. Dies kann auch zur Priorisierung von Revisionsprüfungen und Review-Tasks in der Organisation verwendet werden. Das kann bedeuten, dass eine bestimmte ASVS-Anforderung für ein bestimmtes Teammitglied ein Treiber für ein Codereview, ein Refactoring oder eine Auditierung sein kann und als _Technical Debt_ im Backlog sichtbar wird, das zeitnah erledigt werden sollte.

### Als Rahmen für die Steuerung von Dienstleistern zur Erstellung sicherer Software

ASVS ist ein großartiges Rahmenwerk, um bei der sicheren Softwarebeschaffung oder der Beschaffung von kundenspezifischen Entwicklungsdienstleistungen zu unterstützen. Der Auftraggeber kann einfach die Anforderung stellen, dass die Software, die er beschaffen bzw. beauftragen möchte, auf ASVS-Ebene _X_ entwickelt werden muss, und vom Anbieter den Nachweis verlangen, dass die Software die ASVS-Ebene _X_ erfüllt. Dies funktioniert optimal, wenn es mit dem Anhang zum OWASP-Vertrag für sichere Software (_OWASP Secure Software Contract Annex_) kombiniert wird.
