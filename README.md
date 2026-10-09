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
