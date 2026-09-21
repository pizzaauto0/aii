# KiwiGPT — deine lokale KI

Eigenständige Chat-Web-App mit ChatGPT-inspirierter Oberfläche; kein OpenAI-Produkt.

## Starten

Den veröffentlichten Link öffnen: Im Standardmodus wird sofort **KiwiGPT Mini** geladen. Sobald Text im Eingabefeld steht, wechselt der Automatikmodus zu **KiwiGPT Groß** und lädt es. Kein API-Schlüssel und kein kostenpflichtiger KI-Dienst nötig.

Lokal: `python3 -m http.server 8000 --directory dist`, dann `http://localhost:8000` öffnen. Nicht per `file://` starten. Zum Bereitstellen den Inhalt von `dist/` auf einem HTTPS-Static-Host veröffentlichen.

## Modelle

Die Namen in der Oberfläche stehen für drei echte Modellgrößen aus Qwen2.5-Instruct (Apache 2.0), quantisiert für WebLLM:

- **KiwiGPT Mini:** 0,5B, ungefähr 1,1 GB Grafikspeicher, für einfache Fragen.
- **KiwiGPT Normal:** 1,5B, ungefähr 1,9 GB Grafikspeicher, manuell für alltägliche Aufgaben auswählbar.
- **KiwiGPT Groß:** 3B, ungefähr 2,9 GB Grafikspeicher, wird im Automatikmodus beim Schreiben geladen.

WebGPU ist erforderlich. Browser, Treiber und Geräte können die Ausführung einschränken; insbesondere Mobilgeräte können für Normal oder Groß zu wenig Speicher haben. Es gibt keinen simulierten Antwortmodus und keinen versteckten Cloud-Fallback.

Laufzeitcode von esm.run, Modellgewichte von Hugging Face und WASM-Modellbibliotheken aus der WebLLM-Konfiguration werden beim ersten Schreiben oder bei einem Modellwechsel geladen. Die Inferenz erfolgt lokal; die Download-Anbieter sehen die üblichen Netzwerkmetadaten. Der Browser kann Modelldaten zwischenspeichern, aber ein vollständig offlinefähiger App-Start wird nicht garantiert.

## Funktionen und Grenzen

- Automatischer Mini-Download beim Öffnen, automatischer Wechsel zu Groß beim Schreiben, manuelle Modellauswahl, Streaming-Antworten, Stoppen, erneute Antwort, Kopieren, Chatverlauf und Suche.
- Schnell: 192 Ausgabetokens; Ausgewogen: 512; Gründlich: Entwurf und zusätzlicher Prüf-Durchlauf mit je bis zu 768 Tokens. Keine Behauptung, ChatGPT-Reasoning nachzubilden oder zuverlässig bessere Antworten zu garantieren.
- Gerätespeicher statt Konto/Cloud-Sync; JSON-Export und Löschen einzelner Chats.
- Kleine TXT/MD/CSV/JSON-Anhänge, maximal 1.600 Bytes; pro Eingabe insgesamt maximal 2.000 UTF-8-Bytes. Alte Nachrichten werden kontextabhängig weggelassen, um in das 4.096-Token-Fenster zu passen.
- Optionales Diktieren mit separater Zustimmung und Browser-Sprachausgabe. Spracherkennung und manche Stimmen können einen Anbieter kontaktieren. Kein autonomer Echtzeit-Sprachmodus.
- Keine Bildanalyse/-generierung, kein Webzugriff, keine PDF-Verarbeitung. Kleine Modelle sind bei Deutsch, Fakten und komplexen Aufgaben deutlich schwächer als große Modelle.

## Quellen

- https://webllm.mlc.ai/docs/user/basic_usage.html
- https://github.com/mlc-ai/web-llm
- https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct

## Prüfung

JavaScript-Syntax und statische Referenzen können ohne GPU geprüft werden. Echte Modellgenerierung erfordert den Download und ein kompatibles WebGPU-Gerät. Die App zeigt fehlende GPU-Unterstützung sowie Lade- und Generierungsfehler sichtbar an.
