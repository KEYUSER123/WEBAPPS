# GitHub Pages – Finanzplan + Fitness-Tracker

## Struktur

- `index.html` – Startseite mit Links auf beide Apps
- `finanzplan/index.html` – bisherige Finanzplan-App (unverändert übernommen)
- `fitness/index.html` – FORM / FITNESS (unverändert übernommen)
- `.nojekyll` – deaktiviert Jekyll-Verarbeitung für GitHub Pages

## Veröffentlichen

1. Entpacke dieses ZIP auf deinem Computer.
2. Öffne dein bestehendes GitHub-Repository.
3. Lade den **Inhalt** dieses Ordners ins Repository hoch, nicht den äußeren Ordner `github-pages-paket` als zusätzliche Ebene.
4. Wichtig: Die bisherige Finanzplan-`index.html` im Repository-Stamm muss durch die neue Dashboard-`index.html` ersetzt werden. Die bisherige Finanzplan-Datei liegt jetzt unter `finanzplan/index.html`.
5. Committe die Änderungen und warte, bis GitHub Pages neu veröffentlicht hat.
6. Öffne die Website-URL deines Repositories. Von der Startseite aus führen die Kacheln zu beiden Apps.

Wenn GitHub Pages auf `main` und `/(root)` eingestellt ist, sollte diese Ordnerstruktur direkt funktionieren.

## Hinweise

- Die App-Dateien wurden inhaltlich nicht umgebaut; sie wurden nur in eigene Ordner gelegt.
- Die Finanzplan-App enthält eine Supabase-Konfiguration. Prüfe in Supabase die erlaubten Redirect-URLs/URLs deiner Website, falls die Anmeldung nach dem Verschieben nicht wie erwartet zurückkehrt.
- Beide Apps nutzen `localStorage` mit unterschiedlichen Schlüsseln. Browserdaten bleiben grundsätzlich an die Website-Origin gebunden; sichere wichtige Daten vor größeren Änderungen zusätzlich über die Backup-Funktionen der Apps.
- Dieses Paket richtet noch keine PWA-/Offline-Funktionen ein.


## Gemeinsamer Login und Fitness-Cloud-Speicherung

- Die Dashboard-Startseite verlangt jetzt eine Supabase-Anmeldung. Finanzplan und Fitness verwenden dieselbe Supabase-Projektkonfiguration und denselben Browser-Login.
- Die Fitness-App lädt/speichert ihren bisherigen Gesamtzustand als JSONB in `public.fitness_data`. Die lokale Speicherung im Browser bleibt als Offline-Kopie bestehen.
- **Einmalig vor der Fitness-Cloud-Synchronisierung:** Öffne Supabase → SQL Editor und führe `supabase-fitness-setup.sql` aus. Die Tabelle hat Row Level Security (RLS); jeder angemeldete Benutzer darf nur seine eigene Zeile lesen/schreiben.
- Die Finanzplan-App verwendet weiterhin ihre vorhandene Tabelle `app_data`; diese wird durch das Paket nicht verändert.
- Wenn auf einem Gerät bereits Fitnessdaten liegen und in der Cloud ebenfalls andere Daten gefunden werden, fragt die Fitness-App, welche Version verwendet werden soll. Ohne Cloud-Zeile werden vorhandene lokale Daten beim ersten Start hochgeladen.
- Nach dem Ausführen des SQL: alle Dateien im ZIP-Paket-Ordner in das GitHub-Repository hochladen (nicht den übergeordneten Ordner als zusätzliche Ebene).
- Prüfe beim ersten Test zuerst, ob Login/Logout funktioniert und anschließend, ob ein neu erstelltes Training nach Neuladen und auf einem zweiten Gerät noch vorhanden ist.

## Sicherheitshinweis

Die im Frontend eingetragene Supabase-URL und ein `publishable`/anon-Schlüssel sind für Browser-Apps vorgesehen. Niemals einen `service_role`-Schlüssel in GitHub hochladen. Datensicherheit wird bei dieser Architektur durch Supabase Auth und RLS sichergestellt, nicht durch das Verstecken der Tabellen oder Links.


## Navigation zwischen den Apps
Im Finanzplan und in der Fitness-App befinden sich nun Links zum Dashboard und zur jeweils anderen App. Da alle Seiten unter demselben GitHub-Pages-Ursprung liegen und dieselbe Supabase-Projektkonfiguration verwenden, bleibt die Supabase-Sitzung beim Wechsel grundsätzlich erhalten. Die Links ersetzen keine Authentifizierungs- oder Datenbank-Sicherheitsregeln.
