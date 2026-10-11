# Workspace – Dashboard, Aufgaben, Finanzplan und Fitness

Das Repository ist eine statische Website für GitHub Pages. Es verwendet kein Build-System und keine zusätzliche Paketinstallation. Die Apps teilen sich Supabase Auth, speichern ihre jeweiligen Anwendungsdaten aber in getrennten Tabellen.

## Projektstruktur

- `index.html` – Login und modernes zentrales Dashboard
- `todos/index.html` – ToDo-MVP mit Erstellen, Bearbeiten, Löschen, Status, Priorität, Fälligkeit, Bereich und Filtern
- `finanzplan/index.html` – bestehende Finanzplan-App
- `fitness/index.html` – bestehende FORM / FITNESS-App
- `supabase-todos-setup.sql` – Tabelle, Indizes, Trigger und RLS-Policies für ToDos
- `supabase-fitness-setup.sql` – Cloud-Tabelle und RLS-Policies für Fitnessdaten

## Supabase einmalig einrichten

1. Öffne das richtige Supabase-Projekt und gehe zu **SQL Editor**.
2. Führe den Inhalt von `supabase-todos-setup.sql` aus, um die ToDo-Tabelle `public.todos` einzurichten.
3. Falls die Fitness-Cloud-Tabelle `public.fitness_data` noch nicht existiert, führe ebenfalls `supabase-fitness-setup.sql` aus.
4. Die Finanzplan-App verwendet weiterhin ihre bestehende Tabelle `public.app_data`; dieses Paket ändert deren Schema nicht.
5. Stelle in Supabase unter Authentication die erlaubten Website-/Redirect-URLs für deine veröffentlichte GitHub-Pages-Adresse ein.

Die `todos`-Tabelle nutzt Row Level Security. Ein angemeldeter Nutzer kann nur Zeilen lesen und ändern, bei denen `user_id` seiner eigenen Supabase-User-ID entspricht. Die Frontend-Prüfung ist keine Sicherheitsgrenze; entscheidend sind RLS und die Datenbankrechte.

## Lokal testen

Du kannst die HTML-Dateien direkt im Browser öffnen, für die vollständige Authentifizierung und Cloud-Synchronisierung sollte aber dieselbe Website-Origin über einen lokalen Webserver oder GitHub Pages verwendet werden. Die Projektdateien benötigen keine npm-Installation. Der Supabase-JavaScript-Client wird vom CDN geladen.

## Auf GitHub Pages veröffentlichen

1. Entpacke das Paket.
2. Lade den **Inhalt** des Ordners `WEBAPPS-main` ins Repository hoch, nicht den äußeren Ordner als zusätzliche Ebene.
3. Achte darauf, dass `index.html` im Veröffentlichungsstamm liegt und `todos/`, `finanzplan/` sowie `fitness/` daneben liegen.
4. Committe die Änderungen und warte auf den GitHub-Pages-Deploy.
5. Teste die Anmeldung, das Erstellen und Erledigen einer Aufgabe sowie das Neuladen der ToDo-Seite.

## Funktionsumfang der ToDo-Version

- Persönliche Aufgaben mit Titel und optionaler Beschreibung
- Status: Offen, In Bearbeitung, Erledigt
- Priorität: Niedrig, Mittel, Hoch
- Fälligkeitsdatum und Bereich (Allgemein, Privat, Arbeit, Finanzen, Fitness, Studium)
- Filter: Alle offenen Aufgaben, Heute, Demnächst, Überfällig, Erledigt
- Suche, Dashboard-Kennzahlen und schnelle Erledigung direkt vom Dashboard
- Alle Datensätze sind an den angemeldeten Nutzer gebunden

Wiederholungen, Unteraufgaben und echte Projekt-/Listenbeziehungen sind bewusst nicht Teil des ersten MVP. Dafür kann später ein eigenes Datenmodell ergänzt werden.

## Designrichtung

Das Dashboard kombiniert ruhige Flächen, progressive Offenlegung und reduzierte Navigation, inspiriert von Produktivitäts- und SaaS-Dashboards wie [Linear](https://linear.app/), [Notion](https://www.notion.so/) und den in [SaaSUI Designbeispielen](https://www.saasui.design/blog/best-saas-dashboard-examples) beschriebenen Mustern. Das Ziel ist ein schneller Überblick mit einer klaren nächsten Aktion statt einer überfüllten Startseite.

## Sicherheitshinweise

- Nur den vorgesehenen Supabase Publishable-/anon-Key im Browser verwenden. Niemals einen `service_role`-Key in HTML oder GitHub hochladen.
- Private Tabellen immer mit passenden RLS-Policies absichern.
- Bewahre vor größeren Änderungen zusätzlich eigene Backups auf.
