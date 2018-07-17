---
title: 'Alternativen zu Apache: Nginx'
date: '18-06-2016 02:10'
taxonomy:
    category:
        - blog
    tag:
        - journal
        - test
external_links:
    process: true
    mode: active
twitterenable: false
twittercardoptions: summary
articleenabled: false
facebookenable: false
content:
    items: '@self.children'
    limit: '5'
    order:
        by: date
        dir: desc
    pagination: '1'
---

Alle Jahre wieder rege ich mich über die Verarbeitungsgeschwindigkeit meiner privaten Webseiten auf. So auch wieder vor einigen Tagen. Ich gebe zu, dass es potentere Webserver gibt als meinen Atom 510 mit 4G, aber als Schreibtischserver hat das Ding seine Berechtigung: Die niedrigen Kosten bei 24x7. Natürlich kann man Abhilfe schaffen: Ich könnte meinen Blog, das Wiki, den Bugtracker auch auf die große Maschine bei Strato packen, genau das will ich aber nicht, da ich es als sehr angenehm empfinde, einen Server, auf dem ich alle Updates ausprobieren kann, neben dem Schreibtisch stehen zu haben.

<!--more-->

Wenn das Ding die Hufe hochreisst, dann ist nur ein Teil meiner privaten Seiten nicht erreichbar. Ein Zustand, den ich als sehr beruhigend empfinde. Aufrüsten des Atoms gestaltet sich schwierig, der ist voll ausgebaut, ein AMD E 450 hätte seine Vorteile, kostet aber Geld. Ein energiesparender i3 dito, das wäre mit Kanonen auf Spatzen geschossen. Die einzige Chance, was zu ändern, besteht in der verwendeten Software. Da ich mit lighttpd nicht wirklich gut zurrecht kam, reifte der Plan, auf nginx umzustellen.

Gesagt, getan, eine virtuelle Maschine aufgesetzt und den ersten nginx aufgesetzt. Wenigstens bist zu diesem Punkt waren die Debian-Pakete sinnvoll. Wenige Stunden später waren die ersten Testseiten aufgesetzt und reproduzierbar in Betrieb genommen. Der einzige Knackpunkt war Chiliproject. Ein kurzer Test mit einer Standalone-Kombi passenger und nginx kam auch ganz gut und damit begann das Verhängnis.

Im Gegensatz zum Apachen sind die Module für Nginx nicht separat erhältlich, die werden konfiguriert und einkompiliert. "Natürlich" gilt das auch für alle Settings, Pfade etc. Das hört sich noch gar nicht mal so tragisch an, wird es aber bei näherer Betrachtung:
<ul>
	<li>Was tut man, wenn ausgerechnet eines der wichtigsten Module für den täglichen Betrieb in keinem Debian-Paket auftaucht?</li>
	<li>Wenn das Modul zufällig passenger heisst - dafür gibt es ein debian-Paket, das einem aber bei der Installation auch einen neuen nginx unterschiebt - natürlich ohne die anderen Module, die man mit dem regulären nginx installiert hat.</li>
	<li>Dass dann eine eventuell vorhandene Konfiguration gnadenlos zerhackt wird, ist nur konsequent.</li>
</ul>
Ein möglicher Lösungsansatz ist die Deinstallation des eigentlich sinnvoll vorkonfigurierten Debian-Pakets, die Nutzung es Passenger-Pakets oder einfach der Verzicht auf debian-Pakete ohne wenn und aber. Das hat alles seine Vor- und Nachteile.

Vorteile:
<ul>
	<li>Es funktioniert, wenn nicht, dann sitzt der dafür verantwortliche Trottel direkt vor dem Schirm</li>
	<li>Man ist unabhängig von der manchmal etwas disskussionwürdigen Paketpflege bei debian im Bereich Web.</li>
</ul>
Nachteile:
<ul>
	<li>Man arbeitet am Paketsystem vorbei, man ist auf lokale Bau der Pakete angewiesen. Je nach persönlichem Können nicht unbedingt ein Traumzustand, eher einer für Albträume</li>
	<li>apt-get dist-upgrade greift nicht, ich muss das Zeug manuell aktuell halten. Kompilieren auf einem Atom macht zudem nicht wirklich Spass</li>
	<li>Man muss ein Build-System auf dem Server vorhalten. Nicht wirklich ein schöner Zustand. Das es aber um Ruby geht, braucht man das im Zweifel so oder so, da die benötigten Gems nicht in der Version, die man grade braucht, im debian-Repo vorhanden sein werden.</li>
	<li>Es fällt kein Paket unten raus, man darf auf jeder Installation neu bauen.</li>
</ul>
Alles in allem kein sonderlich befriedigender Zustand, den ich eigentlich mal durch ein eigenes Paket lösen sollte. Noch schöner wäre ein eigenes Paket zu diesem Thema. Da ich aber keinen Plan habe, wie ich das am cleversten umsetze wird es vorerst bei der Scriptanpassung bleiben, ideal wäre natürlich die Änderung direkt in debian.