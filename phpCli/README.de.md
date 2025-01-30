# Lane4 Digital PHP CLI

![Build Status](https://github.com/lane4hub/docker/actions/workflows/phpCli.yml/badge.svg)
[![Docker Image Version](https://img.shields.io/docker/v/lane4hub/phpcli?sort=semver)](https://hub.docker.com/r/lane4hub/phpcli)

### Bereitstellung versionierter PHP-Docker-Images für Konsolenanwendungen

Das **Lane4 Digital PHP CLI**-Tool wurde entwickelt, um plattformübergreifende PHP-CLI-Docker-Images bereitzustellen. Es unterstützt PHP-Versionen von **7.4 bis 8.3** und ermöglicht Entwicklern und Administratoren die Erstellung und Pflege konsistenter und zuverlässiger Umgebungen für ihre Konsolenanwendungen.

Unsere Docker-Images sind für die Architekturen **AMD64** und **ARM64** verfügbar und werden auf [Docker Hub](https://hub.docker.com/r/lane4hub/phpcli) gehostet. Dies gewährleistet eine breite Kompatibilität und ermöglicht die Bereitstellung auf verschiedenen Hardware-Plattformen, darunter moderne Server und IoT-Geräte.

## Funktionen

1. **PHP-Versionen**: Unterstützung verschiedener PHP-Versionen über das Build-Argument `PHP_VERSION`.
  - **Verfügbare Versionen**: 7.4, 8.0, 8.1, 8.2, 8.3

2. **Erweiterungen**: Enthält häufig genutzte PHP-Erweiterungen:
  - `pdo`, `pdo_mysql`, `mysqli` (Datenbankunterstützung)
  - `redis` (Caching)
  - `curl` (HTTP-Anfragen)
  - `soap` (SOAP-Dienste)
  - `dom`, `zip` (Datei- und XML-Verarbeitung)
  - `mbstring` (Mehrbyte-Zeichenkettenverarbeitung)
  - `pcntl` (Multi Prozesse)

3. **Xdebug**:
  - Automatische Installation der passenden Xdebug-Version:
    - Xdebug 3.1.6 für PHP 7.4.
    - Neueste Xdebug-Version für PHP >= 8.0.
  - Aktiviert für Debugging und Profiling.

4. **Composer**:
  - Neueste Version von `composer` ist vorinstalliert und sofort einsatzbereit.

5. **Minimaler Overhead**:
  - Basierend auf `alpine`, einer sehr schlanken Linux-Distribution, um die Image-Größe klein zu halten.

6. **Benutzerfreundliche Konfiguration**:
  - Standardmäßig vorkonfiguriert mit `php.ini` im Produktionsmodus, jedoch leicht anpassbar.

7. **Zweistufiger Build-Prozess**:
  - **Build-Phase**: Installation und Konfiguration von Abhängigkeiten und PHP-Erweiterungen.
  - **Laufzeit-Phase**: Nur essenzielle Dateien werden in die Laufzeitumgebung übernommen, um die Image-Größe zu reduzieren.

## Voraussetzungen

Bitte beachten Sie die Installationsvoraussetzungen in der Datei `README.md`, die sich im Root-Verzeichnis des Docker-Projekt-Repositorys befindet.

## Verwendung

Wir haben ein `Makefile` erstellt, das alle verfügbaren Nutzungsmöglichkeiten über den Befehl `make` im Terminal bereitstellt.

## Anpassung an Ihre Bedürfnisse

Falls Sie das Tool vollständig an Ihre spezifischen Anforderungen anpassen möchten, können Sie die relevanten Einträge in der Datei `.env` bearbeiten.

Dies ermöglicht eine flexible Konfiguration der bereitgestellten Docker-Images, einschließlich spezifischer PHP-Erweiterungen, Konfigurationseinstellungen und weiterer Anpassungen.

Für diese Art der Nutzung benötigen Sie Ihr eigenes Quell- und Image-Repository.

Wir würden es sehr schätzen, wenn Sie uns in solchen Fällen als Unterstützer Ihrer Docker-Images anerkennen würden.

## Inhalt von `phpCli`

Das `phpCli`-Paket enthält die folgenden Komponenten:

- **Quellcode-Dateien**:
  - `/phpcli` – Enthält den Quellcode und die Konfigurationsdateien des PHP-CLI-Tools.

- **Support-Dateien**:
  - `.env` – Umgebungsvariablen zur Konfiguration der Docker-Images.
  - `docker-compose.yml` – Docker-Compose-Konfigurationsdatei zur Orchestrierung der Container.
  - `Dockerfile` – Dockerfile zum Erstellen der PHP-CLI-Images.
  - `Makefile` – Einfache Kommandozeilenhilfe. Führen Sie `make` im Terminal aus, um die verfügbaren Befehle anzuzeigen.
  - `.github/workflows/phpCli.yml` – GitHub Actions Workflow zur Automatisierung von Builds und Tests.

- **Dokumentation**:
  - `README.md` – Umfassende Dokumentation und Anleitungen zur Nutzung des Tools.

## Anwendungsbeispiele

```bash
docker build --build-arg PHP_VERSION=8.1 -t my-php-image .
docker run --rm -v $(pwd):/app -w /app my-php-image php script.php
