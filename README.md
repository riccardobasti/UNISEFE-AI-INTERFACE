# UNISEFE-AI-INTERFACE
AI Interface

https://riccardobasti.github.io/UNISEFE-AI-INTERFACE/

**A lightweight, single-file AI workspace with OpenRouter and local Ollama support.**

UNISEFE AI INTERFACE is an experimental AI workspace designed around a simple idea:

> powerful tools underneath, a simple interface on top.

The application is delivered as a single HTML file and combines chat, local files, history, Viewer, configurable AI providers and the UNISEFE CORE state model.

---

## What is included

- **Single HTML file**
- **UNISEFE AI chat**
- **OpenRouter provider**
- **Ollama local provider**
- **Local model catalog in the Viewer**
- **Install / remove / select Ollama models**
- **Automatic “install and use” flow**
- **Local file workspace**
- **Conversation history**
- **HTML / text / image Viewer**
- **Viewer code mode**
- **UNISEFE CORE**
- **SEFTY support**
- **Connector architecture**
- **No localStorage for persistent project data**

---

## Ollama local models

UNISEFE can use Ollama as a local AI backend.

The user keeps the UNISEFE interface while Ollama runs the selected model locally:

```text
UNISEFE AI INTERFACE
        ↓
      Ollama
        ↓
   Local AI model
```

### Model catalog

The Viewer contains a simple local-model catalog.

Each model can show useful information such as:

- model name
- approximate download size
- intended use
- context information
- estimated suitability for the current computer
- installation state

The goal is not to expose dozens of technical parameters.  
The user should only see the information needed to make a practical choice.

### Install and use

A model has a simple **Use** action.

If the model is already installed, UNISEFE selects it immediately.

If the model is not installed, UNISEFE asks whether it should be installed first. After installation completes, the same model becomes active automatically.

```text
Use
 ↓
Already installed?
 ├─ Yes → activate model
 └─ No  → ask permission → install → activate model
```

Models can also be installed or removed directly from the catalog.

### Local endpoint

UNISEFE talks to the local Ollama service at:

```text
http://localhost:11434
```

The current integration uses Ollama's local API for:

- listing installed models
- pulling models
- deleting models
- chatting with the selected model

Ollama itself must already be installed and running on the computer.

---

## OpenRouter

OpenRouter remains available as an alternative provider.

The user can switch between:

```text
OpenRouter
Ollama local
```

OpenRouter uses the configured API key and model.  
Ollama uses the selected model running on the user's own computer.

---

## UNISEFE CORE

The interface includes the UNISEFE CORE state model:

```text
BYTE
VALUE
CHAINS
DELTA
BIT
```

The application keeps one shared live Space for UI state, files, history, Viewer state, AI configuration and connectors.

Persistent user data is written to files in the selected UNISEFE workspace rather than stored in `localStorage`.

---

## Local workspace

UNISEFE can work with a user-selected folder.

Current workspace functions include:

- list files
- read files
- create files
- create folders
- upload files
- overwrite files with confirmation
- open supported files in the Viewer

The Viewer supports:

- text
- HTML
- images
- source/code view

---

## AI tools and connectors

The AI layer can expose selected UNISEFE functions as tools, including file and history operations.

The connector architecture is designed so additional services can be added without rebuilding the whole interface.

The project also includes a local Viewer bridge for controlled interaction with HTML applications opened inside the Viewer.

---

## Philosophy

UNISEFE AI INTERFACE is intentionally small.

The project does not aim to reproduce every setting exposed by AI runtimes or commercial dashboards.

The design rule is:

> **keep only what people actually need.**

Local models should feel like normal applications:

```text
choose model → install → use
```

The technical complexity stays underneath the interface.

---

## Current status

**Alpha / experimental software**

The project is under active development.

Some browser capabilities depend on browser support and local permissions. Ollama integration requires a reachable local Ollama service.

Do not treat the project as production-ready security software.

---

## Quick start

1. Download the latest UNISEFE AI HTML file.
2. Open it in a compatible browser.
3. Open or choose your UNISEFE workspace folder.
4. Open the **AI** panel.
5. Choose either **OpenRouter** or **Ollama local**.
6. For Ollama, make sure Ollama is installed and running.
7. Open **Local models**.
8. Choose a model and press **Use**.
9. If necessary, approve the model download.
10. Chat from the normal UNISEFE interface.

---

## Why Ollama + UNISEFE?

Ollama handles local model execution.

UNISEFE handles the user environment.

```text
Ollama  = local AI engine
UNISEFE = interface + files + history + Viewer + tools + workspace
```

This separation lets UNISEFE stay independent from any single AI model.

A user can use a local Ollama model today and another provider tomorrow without changing the workspace or the way the interface is used.

---

## Repository

**UNISEFE AI INTERFACE**

https://github.com/riccardobasti/UNISEFE-AI-INTERFACE

---

# Italiano

## UNISEFE AI INTERFACE

UNISEFE AI INTERFACE è un workspace AI sperimentale, leggero e contenuto in un singolo file HTML.

L'obiettivo è semplice:

> **potenza sotto, semplicità sopra.**

L'interfaccia riunisce chat, file locali, storico, Viewer, provider AI configurabili e UNISEFE CORE.

### Funzione Ollama

UNISEFE può usare **Ollama come motore AI locale**.

L'utente continua a usare la normale interfaccia UNISEFE:

```text
UNISEFE AI INTERFACE
        ↓
      Ollama
        ↓
  modello AI locale
```

Nel Viewer è disponibile un catalogo essenziale dei modelli locali, con le informazioni utili per scegliere quale modello usare.

Per ogni modello possono essere mostrati:

- nome
- dimensione approssimativa
- utilizzo principale
- contesto
- compatibilità stimata con il PC
- stato di installazione

### Usa

Il pulsante **Usa** mantiene il flusso il più semplice possibile.

Se il modello è già installato, viene selezionato.

Se non è installato, UNISEFE chiede il permesso, avvia il download tramite Ollama e, una volta completato, rende automaticamente quel modello attivo.

```text
Usa
 ↓
Modello installato?
 ├─ Sì → attiva
 └─ No → chiedi → installa → attiva
```

È inoltre possibile installare e rimuovere i modelli direttamente dal catalogo.

### Importante

La funzione attuale **non installa il programma Ollama nel sistema operativo**.

Ollama deve essere già installato e in esecuzione sul computer.  
UNISEFE gestisce invece i **modelli Ollama** attraverso il servizio locale:

```text
http://localhost:11434
```

### Provider disponibili

Attualmente l'interfaccia può usare:

```text
OpenRouter
Ollama locale
```

Questo permette di mantenere la stessa chat e lo stesso workspace cambiando soltanto il motore AI.

---

## Principio del progetto

UNISEFE non vuole diventare un pannello pieno di opzioni inutili.

La regola è:

> **se una funzione non serve davvero all'utente, non entra.**

Per i modelli locali il flusso ideale rimane:

```text
scegli → installa → usa
```

Tutto il resto deve rimanere sotto il cofano.

---

**Project:** UNISEFE  
**Repository:** `riccardobasti/UNISEFE-AI-INTERFACE`  
**Status:** Alpha / Experimental
