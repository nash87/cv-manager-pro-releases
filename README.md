# CV Manager Pro

<div align="center">

![Version](https://img.shields.io/badge/version-1.1.3-blue)
![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11-brightgreen)
![License](https://img.shields.io/badge/license-Proprietary-red)
![Security](https://img.shields.io/badge/security-AES--256--GCM-green)
![GDPR](https://img.shields.io/badge/GDPR-compliant-success)

**Professional CV Management with Military-Grade Encryption**

[🇩🇪 Deutsch](#-deutsch) | [🇬🇧 English](#-english) | [📥 Download](#-download)

</div>

---

## 🇩🇪 Deutsch

### 📑 Inhaltsverzeichnis

- [Überblick](#überblick)
- [Features](#features)
- [Download & Installation](#download--installation)
- [Technische Architektur](#technische-architektur)
  - [Backend](#backend)
  - [Frontend](#frontend)
  - [Datenverschlüsselung](#datenverschlüsselung)
- [Sicherheit & Datenschutz](#sicherheit--datenschutz)
  - [Verschlüsselung](#verschlüsselung)
  - [DSGVO-Konformität](#dsgvo-konformität)
- [Systemanforderungen](#systemanforderungen)
- [FAQ](#faq)
- [Support](#support)

---

### Überblick

**CV Manager Pro** ist eine professionelle Desktop-Anwendung für die sichere Verwaltung und Erstellung von Lebensläufen. Alle Daten werden lokal auf Ihrem Computer gespeichert und mit militärischer AES-256-GCM-Verschlüsselung geschützt.

#### Warum CV Manager Pro?

- **🔒 Absolute Privatsphäre**: Keine Cloud, keine Server - Ihre Daten bleiben auf Ihrem PC
- **🛡️ Militärische Verschlüsselung**: AES-256-GCM mit PBKDF2 Key Derivation
- **⚖️ DSGVO-konform**: Volle Kontrolle, Datenexport, Löschfunktionen
- **🎨 Moderne UI**: Obsidian-inspiriertes, kompaktes Design
- **📊 Visualisierung**: Interaktive Charts und Timeline-Ansichten
- **📄 PDF-Export**: Professionelle CVs direkt als PDF exportieren

---

### Features

#### 🎯 Kernfunktionen

- **CV-Verwaltung**: Mehrere CVs parallel verwalten und organisieren
- **Quick Create**: Schnelles Erstellen neuer CVs mit Vorlagen
- **Visual Editor**: Live-Bearbeitung mit Echtzeit-Vorschau
- **Smart Search**: Durchsuchen Sie alle CVs mit Volltext-Suche
- **Export/Import**: DSGVO-konforme Datenexporte und -importe
- **PDF Generation**: Hochwertige PDF-Exports Ihrer Lebensläufe

#### 🎨 Benutzeroberfläche

- **Dashboard**: Übersichtliche Darstellung aller CVs
- **Quick Actions**: Schnellzugriff auf häufige Aktionen
- **Statistiken**: Visualisierung Ihrer CV-Daten mit Chart.js
- **Updates**: Integrierte Versionshistorie und Changelog
- **Consent Screen**: DSGVO-konformer Onboarding-Prozess
- **Custom Titlebar**: Native Window-Controls (Minimize/Maximize/Close)

#### 🔐 Sicherheit

- **End-to-End Verschlüsselung**: Alle Daten verschlüsselt gespeichert
- **Master Password**: Ein sicheres Passwort schützt alle Ihre Daten
- **Automatic Migration**: Sichere Datenbankmigration bei Updates
- **Database Repair**: Automatische Reparatur bei Korruption
- **No Telemetry**: Keine Datenübertragung, keine Tracker

---

### Download & Installation

#### 📥 Download

**Aktuelle Version: v1.1.3** (26. Dezember 2025)

[![Download](https://img.shields.io/badge/Download-cv--manager--pro.exe-blue?style=for-the-badge&logo=windows)](https://github.com/nash87/cv-manager-pro-releases/releases/download/v1.1.3/cv-manager-pro.exe)

- **Größe**: 16 MB
- **SHA256**: `4245453fe27d82ffa5855e16a887e54328dbc27aed36eecf9574fe15cb276269`

#### 🔧 Installation

1. **Herunterladen**: Laden Sie `cv-manager-pro.exe` herunter
2. **WebView2**: Stellen Sie sicher, dass Microsoft Edge WebView2 Runtime installiert ist
   - Download: [WebView2 Runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/)
3. **Ausführen**: Starten Sie `cv-manager-pro.exe`
4. **Master Password**: Wählen Sie ein sicheres Master-Passwort
5. **Consent**: Akzeptieren Sie die Datenschutzerklärung

---

### Technische Architektur

#### Backend

**Technologie-Stack:**
- **Sprache**: Go 1.23+
- **Framework**: Wails v2.11.0 (Go + WebView2)
- **Datenbank**: BadgerDB v4.2.0 (LSM-Tree embedded database)
- **Verschlüsselung**: AES-256-GCM (Go standard library `crypto/aes`)
- **Key Derivation**: PBKDF2 mit 100.000 Iterationen (SHA-256)

**Komponenten:**

```
app.go                  - Hauptanwendungslogik, Wails-Integration
encrypted_storage.go    - BadgerDB mit AES-256-GCM Verschlüsselung
cv_manager.go          - CV-Verwaltung (CRUD-Operationen)
version.go             - Versionsverwaltung und Changelog
migration.go           - Automatische Datenbankmigrationen
```

**BadgerDB Konfiguration:**
- **IndexCacheSize**: 100 MB (erforderlich für verschlüsselte Workloads)
- **ValueLogFileSize**: 64 MB (verhindert riesige vlog-Dateien)
- **NumVersionsToKeep**: 1 (minimale Speichernutzung)
- **CompactL0OnClose**: true (automatische Komprimierung)

#### Frontend

**Technologie-Stack:**
- **UI Framework**: Vanilla JavaScript (ES6+)
- **Charting**: Chart.js 4.4.1
- **Styling**: Custom CSS mit Obsidian-inspiriertem Design
- **Runtime**: Microsoft Edge WebView2

**Struktur:**

```
index.html    - Hauptstruktur, Views, Modals
app.js        - UI-Logik, Event-Handler, API-Calls
style.css     - Styling, Obsidian-Theme, Kompaktes Layout
```

**Design-Prinzipien:**
- **Kompakt**: 11-13px Fonts, minimale Paddings
- **Konsistent**: Einheitliches Farbschema und Spacing
- **Responsiv**: Anpassung an verschiedene Fenstergrößen
- **Accessibility**: Klare Kontraste, lesbare Schriften

#### Datenverschlüsselung

**Verschlüsselungs-Flow:**

```
Master Password (User)
    ↓
PBKDF2 (100k iterations, SHA-256)
    ↓
256-bit AES Key
    ↓
AES-256-GCM Encryption
    ↓
BadgerDB (encrypted at rest)
```

**Sicherheitsmerkmale:**
- **Salt**: Statischer Salt `cv-manager-pro-salt-v1` (bei Bedarf anpassbar)
- **PBKDF2 Iterations**: 100.000 (optimaler Balance zwischen Sicherheit und Performance)
- **GCM Mode**: Authenticated Encryption (AEAD) verhindert Manipulationen
- **Key Rotation**: Automatische Rotation alle 30 Tage (konfigurierbar)

---

### Sicherheit & Datenschutz

#### Verschlüsselung

**Warum AES-256-GCM?**
- **Military-Grade**: Verwendet von NSA für TOP SECRET-Daten
- **AEAD**: Authenticated Encryption with Associated Data
- **Performance**: Hardware-beschleunigt auf modernen CPUs
- **Standard**: NIST-zertifiziert, weit verbreitet

**Was wird verschlüsselt?**
- ✅ Alle CV-Daten (Name, Kontakt, Erfahrung, Bildung, etc.)
- ✅ Metadaten (Erstellungsdatum, Tags, Notizen)
- ✅ Benutzereinstellungen und Präferenzen
- ✅ Exportierte Backups

**Was wird NICHT verschlüsselt?**
- ❌ Versionsinformationen (öffentlich verfügbar)
- ❌ Changelog (öffentlich auf GitHub)

#### DSGVO-Konformität

**Art. 5 DSGVO - Grundsätze:**
- ✅ **Rechtmäßigkeit**: Explizite Einwilligung beim ersten Start
- ✅ **Zweckbindung**: Daten nur für CV-Verwaltung verwendet
- ✅ **Datenminimierung**: Nur notwendige Daten gespeichert
- ✅ **Richtigkeit**: Benutzer hat volle Kontrolle über Daten
- ✅ **Speicherbegrenzung**: Benutzer kann Daten jederzeit löschen
- ✅ **Integrität & Vertraulichkeit**: AES-256-GCM Verschlüsselung

**Art. 15-22 DSGVO - Betroffenenrechte:**
- ✅ **Art. 15**: Auskunftsrecht (Export-Funktion)
- ✅ **Art. 16**: Berichtigungsrecht (Edit-Funktionen)
- ✅ **Art. 17**: Löschrecht ("Alle Daten löschen"-Button)
- ✅ **Art. 20**: Datenportabilität (JSON-Export)

**Datenspeicherung:**
- **Speicherort**: Lokal auf dem PC des Benutzers
- **Keine Cloud**: Keine Übertragung zu externen Servern
- **Keine Telemetrie**: Keine Nutzungsdaten gesammelt
- **Kein Tracking**: Keine Analytics, keine Cookies

---

### Systemanforderungen

#### Minimum

- **Betriebssystem**: Windows 10 (Version 1809 oder höher)
- **Prozessor**: Intel Core i3 / AMD Ryzen 3
- **RAM**: 4 GB
- **Speicherplatz**: 50 MB (+ Platz für Ihre CV-Daten)
- **WebView2**: Microsoft Edge WebView2 Runtime

#### Empfohlen

- **Betriebssystem**: Windows 11
- **Prozessor**: Intel Core i5 / AMD Ryzen 5 oder besser
- **RAM**: 8 GB oder mehr
- **Speicherplatz**: 100 MB (+ Platz für Backups)
- **Display**: 1920x1080 oder höher

---

### FAQ

**Q: Wo werden meine Daten gespeichert?**
A: Alle Daten werden lokal in `%APPDATA%\cv-manager-pro\` gespeichert. Keine Cloud, keine Server.

**Q: Was passiert, wenn ich mein Master-Passwort vergesse?**
A: Ohne das Master-Passwort können die Daten nicht entschlüsselt werden. Es gibt keine Wiederherstellungsmöglichkeit - bitte bewahren Sie Ihr Passwort sicher auf!

**Q: Kann ich meine Daten exportieren?**
A: Ja! Über Settings → Export können Sie alle Daten als JSON exportieren (DSGVO Art. 20).

**Q: Ist die Software Open Source?**
A: Nein, CV Manager Pro ist proprietäre Software. Dieses Repository dient nur für Releases und Updates.

**Q: Werden meine Daten an Dritte weitergegeben?**
A: Nein! Absolut keine Datenübertragung. Alles bleibt auf Ihrem PC.

**Q: Wie kann ich die App aktualisieren?**
A: Updates werden automatisch beim Start geprüft (via GitHub). Sie können neue Versionen direkt von GitHub herunterladen.

**Q: Läuft die App auf macOS oder Linux?**
A: Aktuell nur Windows. macOS/Linux-Support ist für zukünftige Versionen geplant.

---

### Support

- **Issues**: [GitHub Issues](https://github.com/nash87/cv-manager-pro-releases/issues)
- **Releases**: [GitHub Releases](https://github.com/nash87/cv-manager-pro-releases/releases)
- **Version Info**: [version.json](https://github.com/nash87/cv-manager-pro-releases/blob/main/version.json)

---

## 🇬🇧 English

### 📑 Table of Contents

- [Overview](#overview-1)
- [Features](#features-1)
- [Download & Installation](#download--installation-1)
- [Technical Architecture](#technical-architecture)
  - [Backend](#backend-1)
  - [Frontend](#frontend-1)
  - [Data Encryption](#data-encryption)
- [Security & Privacy](#security--privacy)
  - [Encryption](#encryption)
  - [GDPR Compliance](#gdpr-compliance)
- [System Requirements](#system-requirements)
- [FAQ](#faq-1)
- [Support](#support-1)

---

### Overview

**CV Manager Pro** is a professional desktop application for secure management and creation of curriculum vitae (CVs). All data is stored locally on your computer and protected with military-grade AES-256-GCM encryption.

#### Why CV Manager Pro?

- **🔒 Absolute Privacy**: No cloud, no servers - your data stays on your PC
- **🛡️ Military-Grade Encryption**: AES-256-GCM with PBKDF2 key derivation
- **⚖️ GDPR Compliant**: Full control, data export, deletion features
- **🎨 Modern UI**: Obsidian-inspired, compact design
- **📊 Visualization**: Interactive charts and timeline views
- **📄 PDF Export**: Professional CVs directly as PDF

---

### Features

#### 🎯 Core Functions

- **CV Management**: Manage and organize multiple CVs in parallel
- **Quick Create**: Rapidly create new CVs with templates
- **Visual Editor**: Live editing with real-time preview
- **Smart Search**: Search all CVs with full-text search
- **Export/Import**: GDPR-compliant data exports and imports
- **PDF Generation**: High-quality PDF exports of your CVs

#### 🎨 User Interface

- **Dashboard**: Clear overview of all CVs
- **Quick Actions**: Fast access to frequent actions
- **Statistics**: Visualization of your CV data with Chart.js
- **Updates**: Integrated version history and changelog
- **Consent Screen**: GDPR-compliant onboarding process
- **Custom Titlebar**: Native window controls (Minimize/Maximize/Close)

#### 🔐 Security

- **End-to-End Encryption**: All data stored encrypted
- **Master Password**: One secure password protects all your data
- **Automatic Migration**: Secure database migration during updates
- **Database Repair**: Automatic repair on corruption
- **No Telemetry**: No data transmission, no trackers

---

### Download & Installation

#### 📥 Download

**Current Version: v1.1.3** (December 26, 2025)

[![Download](https://img.shields.io/badge/Download-cv--manager--pro.exe-blue?style=for-the-badge&logo=windows)](https://github.com/nash87/cv-manager-pro-releases/releases/download/v1.1.3/cv-manager-pro.exe)

- **Size**: 16 MB
- **SHA256**: `4245453fe27d82ffa5855e16a887e54328dbc27aed36eecf9574fe15cb276269`

#### 🔧 Installation

1. **Download**: Download `cv-manager-pro.exe`
2. **WebView2**: Ensure Microsoft Edge WebView2 Runtime is installed
   - Download: [WebView2 Runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/)
3. **Run**: Start `cv-manager-pro.exe`
4. **Master Password**: Choose a secure master password
5. **Consent**: Accept the privacy policy

---

### Technical Architecture

#### Backend

**Technology Stack:**
- **Language**: Go 1.23+
- **Framework**: Wails v2.11.0 (Go + WebView2)
- **Database**: BadgerDB v4.2.0 (LSM-Tree embedded database)
- **Encryption**: AES-256-GCM (Go standard library `crypto/aes`)
- **Key Derivation**: PBKDF2 with 100,000 iterations (SHA-256)

**Components:**

```
app.go                  - Main application logic, Wails integration
encrypted_storage.go    - BadgerDB with AES-256-GCM encryption
cv_manager.go          - CV management (CRUD operations)
version.go             - Version management and changelog
migration.go           - Automatic database migrations
```

**BadgerDB Configuration:**
- **IndexCacheSize**: 100 MB (required for encrypted workloads)
- **ValueLogFileSize**: 64 MB (prevents huge vlog files)
- **NumVersionsToKeep**: 1 (minimal storage usage)
- **CompactL0OnClose**: true (automatic compression)

#### Frontend

**Technology Stack:**
- **UI Framework**: Vanilla JavaScript (ES6+)
- **Charting**: Chart.js 4.4.1
- **Styling**: Custom CSS with Obsidian-inspired design
- **Runtime**: Microsoft Edge WebView2

**Structure:**

```
index.html    - Main structure, views, modals
app.js        - UI logic, event handlers, API calls
style.css     - Styling, Obsidian theme, compact layout
```

**Design Principles:**
- **Compact**: 11-13px fonts, minimal paddings
- **Consistent**: Uniform color scheme and spacing
- **Responsive**: Adapts to different window sizes
- **Accessibility**: Clear contrasts, readable fonts

#### Data Encryption

**Encryption Flow:**

```
Master Password (User)
    ↓
PBKDF2 (100k iterations, SHA-256)
    ↓
256-bit AES Key
    ↓
AES-256-GCM Encryption
    ↓
BadgerDB (encrypted at rest)
```

**Security Features:**
- **Salt**: Static salt `cv-manager-pro-salt-v1` (customizable if needed)
- **PBKDF2 Iterations**: 100,000 (optimal balance between security and performance)
- **GCM Mode**: Authenticated Encryption (AEAD) prevents tampering
- **Key Rotation**: Automatic rotation every 30 days (configurable)

---

### Security & Privacy

#### Encryption

**Why AES-256-GCM?**
- **Military-Grade**: Used by NSA for TOP SECRET data
- **AEAD**: Authenticated Encryption with Associated Data
- **Performance**: Hardware-accelerated on modern CPUs
- **Standard**: NIST-certified, widely adopted

**What is encrypted?**
- ✅ All CV data (name, contact, experience, education, etc.)
- ✅ Metadata (creation date, tags, notes)
- ✅ User settings and preferences
- ✅ Exported backups

**What is NOT encrypted?**
- ❌ Version information (publicly available)
- ❌ Changelog (public on GitHub)

#### GDPR Compliance

**Art. 5 GDPR - Principles:**
- ✅ **Lawfulness**: Explicit consent on first launch
- ✅ **Purpose Limitation**: Data only used for CV management
- ✅ **Data Minimization**: Only necessary data stored
- ✅ **Accuracy**: User has full control over data
- ✅ **Storage Limitation**: User can delete data anytime
- ✅ **Integrität & Confidentiality**: AES-256-GCM encryption

**Art. 15-22 GDPR - Data Subject Rights:**
- ✅ **Art. 15**: Right of access (Export function)
- ✅ **Art. 16**: Right to rectification (Edit functions)
- ✅ **Art. 17**: Right to erasure ("Delete all data" button)
- ✅ **Art. 20**: Right to data portability (JSON export)

**Data Storage:**
- **Location**: Locally on the user's PC
- **No Cloud**: No transmission to external servers
- **No Telemetry**: No usage data collected
- **No Tracking**: No analytics, no cookies

---

### System Requirements

#### Minimum

- **Operating System**: Windows 10 (Version 1809 or higher)
- **Processor**: Intel Core i3 / AMD Ryzen 3
- **RAM**: 4 GB
- **Storage**: 50 MB (+ space for your CV data)
- **WebView2**: Microsoft Edge WebView2 Runtime

#### Recommended

- **Operating System**: Windows 11
- **Processor**: Intel Core i5 / AMD Ryzen 5 or better
- **RAM**: 8 GB or more
- **Storage**: 100 MB (+ space for backups)
- **Display**: 1920x1080 or higher

---

### FAQ

**Q: Where is my data stored?**
A: All data is stored locally in `%APPDATA%\cv-manager-pro\`. No cloud, no servers.

**Q: What happens if I forget my master password?**
A: Without the master password, the data cannot be decrypted. There is no recovery option - please keep your password safe!

**Q: Can I export my data?**
A: Yes! Via Settings → Export you can export all data as JSON (GDPR Art. 20).

**Q: Is the software open source?**
A: No, CV Manager Pro is proprietary software. This repository is only for releases and updates.

**Q: Is my data shared with third parties?**
A: No! Absolutely no data transmission. Everything stays on your PC.

**Q: How can I update the app?**
A: Updates are automatically checked on startup (via GitHub). You can download new versions directly from GitHub.

**Q: Does the app run on macOS or Linux?**
A: Currently Windows only. macOS/Linux support is planned for future versions.

---

### Support

- **Issues**: [GitHub Issues](https://github.com/nash87/cv-manager-pro-releases/issues)
- **Releases**: [GitHub Releases](https://github.com/nash87/cv-manager-pro-releases/releases)
- **Version Info**: [version.json](https://github.com/nash87/cv-manager-pro-releases/blob/main/version.json)

---

## 📥 Download

### Latest Release: v1.1.3

[![Download for Windows](https://img.shields.io/badge/Download-Windows%2010%2F11-0078D4?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/nash87/cv-manager-pro-releases/releases/download/v1.1.3/cv-manager-pro.exe)

**File Details:**
- **Filename**: `cv-manager-pro.exe`
- **Size**: 16 MB
- **Platform**: Windows 10/11 (x64)
- **Release Date**: December 26, 2025
- **SHA256**: `4245453fe27d82ffa5855e16a887e54328dbc27aed36eecf9574fe15cb276269`

### Changelog

**v1.1.3 (2025-12-26)**
- ✨ Custom titlebar with minimize/maximize/close buttons
- ✨ Footer with version and copyright info
- 🎨 Obsidian-style UI (compact, smaller fonts)
- 🐛 Improved onboarding error handling
- 🐛 Fixed version loading in Updates view
- 🐛 Optimized exit button styling

[View all releases →](https://github.com/nash87/cv-manager-pro-releases/releases)

---

<div align="center">

**Made with ❤️ using Go + Wails**

© 2025 CV Manager Pro | Encrypted & GDPR Compliant

</div>
