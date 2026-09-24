# UNISEFE-AI-INTERFACE
AI Interface con Openrouter

> **A local-first, single-file AI workspace built around UNISEFE CORE.**

![Status](https://img.shields.io/badge/status-alpha-orange)
![Version](https://img.shields.io/badge/version-0.0.46--alpha-blue)
![Core](https://img.shields.io/badge/core-UNISEFE%20CORE-black)
![Architecture](https://img.shields.io/badge/state-BYTE%20%2F%20VALUE%20%2F%20CHAINS%20%2F%20DELTA%20%2F%20BIT-purple)
![Format](https://img.shields.io/badge/format-single--file%20HTML-green)
![Runtime](https://img.shields.io/badge/runtime-browser-lightgrey)

---

## What is UNISEFE AI INTERFACE?

**UNISEFE AI INTERFACE** is an experimental browser-based environment that brings together:

- AI chat
- local files
- conversation history
- live HTML viewing
- source editing
- local application interaction
- configurable AI providers
- connectors
- SEFTY extensions
- the canonical **UNISEFE CORE Space**

inside one compact interface.

The current application is distributed as a **single HTML file**.

No traditional application backend is required for the local workspace itself.

```text
UNISEFE AI
│
├── FILES
├── HISTORY
├── AI
├── SEFTY
├── SPACE
├── VIEWER
└── CHAT
```

The interface is intentionally designed so that the user can work with AI, files and applications without constantly leaving the same workspace.

---

# Core idea

UNISEFE AI INTERFACE is not only a chat window.

It is a workspace built around one canonical live state:

```text
BYTE
VALUE
CHAINS
DELTA
BIT
```

The embedded UNISEFE CORE maintains nodes in a single `Space`.

Conceptually:

```text
BYTE    = canonical identity
VALUE   = current dynamic value
CHAINS  = dependencies
DELTA   = change state
BIT     = closed / stable state
REV     = revision counter
```

A node is created once and then updated through its VALUE.

```text
identity remains
      ↓
VALUE changes
      ↓
DELTA opens
      ↓
dependent CHAINS are notified
      ↓
BIT closes again
```

The goal is to preserve identity and dependency structure instead of rebuilding unrelated state every time something changes.

---

# Interface

The application uses four main visual areas.

```text
┌──────┬──────────────┬──────────────────────────┬─────────────────────┐
│ RAIL │ SIDE PANEL   │ VIEWER                   │ CHAT                │
│      │              │                          │                     │
│ U    │ Files        │ HTML                     │ UNISEFE AI          │
│ ▱    │ History      │ Source                   │                     │
│ ◴    │ AI           │ Images                   │ messages            │
│ AI   │ SEFTY        │ Local apps               │                     │
│ S    │ Space        │ External pages           │ composer            │
│ Δ    │              │                          │                     │
└──────┴──────────────┴──────────────────────────┴─────────────────────┘
```

The side panel, Viewer and Chat can be opened and closed independently.

This keeps the workspace compact while allowing very different layouts:

```text
files + viewer + chat
history + chat
viewer only
chat only
space + viewer
```

---

# Files

UNISEFE AI can work directly with a user-selected local folder.

When supported by the browser, the interface opens the folder in **read/write mode** through the File System Access API.

Available operations include:

- open folder
- refresh
- create file
- create folder
- upload file
- read file
- overwrite an existing file after confirmation
- inspect the folder tree
- automatically refresh on supported browsers when filesystem notifications are available

If native read/write folder access is not available, the interface can fall back to a **read-only folder import**.

The visible file tree remains part of the live Space.

```text
filesystem
    ↓
fs/tree
    ↓
ui/files
```

Private internal files under `.unisefe` are not exposed as ordinary user paths.

---

# Local persistence

Configuration and history can live inside the selected workspace.

```text
PROJECT/
│
├── user files...
│
└── .unisefe/
    ├── config.json
    └── history/
```

This keeps project state close to the files the user is actually working with.

The current interface does not require a separate traditional database for this local workflow.

---

# History

UNISEFE AI includes persistent conversation history.

A current conversation can be stored inside the `.unisefe/history/` structure and later reopened in the normal chat interface.

The history system is intended to preserve conversations as workspace data rather than as a second disconnected chat product.

Conceptually:

```text
YEAR
└── MONTH
    └── DAY
        └── CHAT
```

The interface can create a new conversation and switch between saved conversations while retaining the same overall workspace.

---

# AI

The current interface includes **OpenRouter** integration.

The AI panel provides configuration for:

```text
MODEL
API KEY
INTERNET ON / OFF
```

The default model field in the current alpha is:

```text
openrouter/free
```

The AI layer is kept separate from UNISEFE CORE.

```text
UNISEFE CORE = state and workspace
AI provider  = intelligence service
```

This means the interface is not architecturally tied to a single model.

---

# Tool / connector system

UNISEFE AI exposes a connector registry.

A connector can register tools that become available to the AI layer.

Conceptually:

```text
CONNECTOR
   ↓
TOOLS
   ↓
AI
   ↓
authorized operation
```

The application publishes a runtime API through:

```javascript
window.UNISEFE
```

including access to:

```text
SPACE
files
history
config
viewer
sefty
connectors
capabilities
```

This makes the interface extensible without replacing the core workspace.

---

# Viewer

The Viewer is a central part of the environment.

It can display:

- text files
- source code
- HTML
- images
- locally selected media
- supported external HTTP(S) pages

For text and HTML files, the user can switch between:

```text
VISUALIZZA
CODICE
```

When editing source in the Viewer, the current file can be saved back to the selected folder when the workspace is opened read/write.

---

# Live HTML Viewer

Local HTML applications opened in the Viewer can optionally expose a controlled interaction layer to the AI.

The embedded Viewer agent supports a limited set of actions:

```text
observe
click
point
type
key
```

This allows the AI to inspect the visible structure of a **local HTML application** and interact with permitted elements.

The agent deliberately excludes protected elements such as:

- password fields
- file inputs
- hidden fields
- one-time-code fields
- explicitly private / secret elements

It also blocks actions on elements considered potentially navigational or sensitive in this local interaction layer.

The first use requires explicit session authorization.

```text
LOCAL HTML
    ↓
Viewer agent
    ↓
controlled DOM observation/actions
    ↓
connector
    ↓
AI
```

External websites remain outside this local action agent.

---

# Viewer Browser

The Viewer also includes a browser-oriented connector.

It can open:

```text
HTTP(S) URL
or
local workspace file
```

inside the same Viewer.

External websites may refuse iframe embedding because of their own security policy.

When that happens, the interface can provide an option to open the address in a separate browser tab.

The current browser connector does **not** give the local Viewer agent permission to operate external websites.

---

# SEFTY

UNISEFE AI can discover SEFTY components from:

```text
/SEFTY/
```

SEFTY is treated as an extension layer rather than as replacement application state.

The current UI bridge exposes a deliberately small set of operations, including configuration access and controlled composer insertion.

One example already supported is emoji insertion into the chat composer without automatically sending a message.

```text
SEFTY
  ↓
UI bridge
  ↓
controlled action
```

---

# Chat

The chat remains permanently integrated with the workspace.

The composer supports:

- multiline text
- Enter to send
- Shift+Enter for a new line
- dynamic textarea height

Assistant responses can render common Markdown structures such as:

- headings
- paragraphs
- lists
- code blocks
- inline code
- tables
- blockquotes

The chat is therefore usable both as a conversational interface and as a technical development surface.

---

# UNISEFE Space panel

The Space panel exposes the current canonical state.

Each node can be inspected as:

```text
BYTE    Δ DELTA    BIT
```

Internally the current alpha keeps:

```text
BYTE
VALUE
CHAINS
DELTA
BIT
REV
```

The Space is the common state layer used by the interface itself.

Examples include:

```text
ui/panel
ui/panel/open
ui/chat/open
ui/viewer/open

fs/tree
fs/root

history/index
history/current

viewer/title
viewer/content
viewer/source
viewer/mode

config/core
ai/status
connectors/index
```

This means interface state, files, history and connectors do not need completely separate state models.

---

# Architecture

```text
                         ┌───────────────────┐
                         │   UNISEFE SPACE   │
                         │                   │
                         │ BYTE              │
                         │ VALUE             │
                         │ CHAINS            │
                         │ DELTA             │
                         │ BIT               │
                         └─────────┬─────────┘
                                   │
          ┌────────────────────────┼────────────────────────┐
          │                        │                        │
          ▼                        ▼                        ▼
      FILESYSTEM                HISTORY                  CONFIG
          │                        │                        │
          └──────────────┬─────────┴─────────┬──────────────┘
                         │                   │
                         ▼                   ▼
                       VIEWER              CHAT
                         │                   │
                         ▼                   ▼
                  LOCAL HTML AGENT        AI PROVIDER
                         │                   │
                         └─────────┬─────────┘
                                   ▼
                              CONNECTORS
```

The important architectural rule is:

> **The interface has one live canonical Space; files remain the visible persistence layer.**

---

# Local-first design

The application is designed around a local workspace first.

This has several practical consequences:

```text
files remain visible
history can remain with the project
configuration can remain with the project
HTML apps can be opened directly
source can be inspected directly
the AI can work beside the actual files
```

The browser becomes the runtime.

The selected folder becomes the workspace.

UNISEFE CORE becomes the shared state.

---

# Security boundaries

The current alpha deliberately separates several levels of authority.

### Local filesystem

Write operations require a workspace opened with read/write permission.

### Existing files

Overwrite is explicit rather than silent.

### Hidden UNISEFE data

Internal `.unisefe` paths are protected from ordinary file operations.

### Viewer agent

Protected fields are excluded.

Local HTML interaction requires session consent.

### External web pages

External pages can be displayed, but the local HTML action agent is not automatically granted control over them.

### AI keys

Provider credentials are configuration data and should never be committed into a public repository.

---

# Capabilities

The current runtime exposes capability information equivalent to:

```text
core: UNISEFE CORE
state: BYTE / VALUE / CHAINS / DELTA / BIT

files: true
history: true
viewer: true
sefty: true
openrouter: true
web: true
connectors: dynamic
filesystem mode: none / ro / rw
```

---

# Current alpha

Current embedded interface version:

```text
0.0.46-alpha
```

The project is experimental.

Browser APIs used by the application are not equally supported by every browser.

In particular, full read/write folder access and filesystem observation depend on browser capabilities.

Fallback behavior is provided where practical.

---

# Design principles

UNISEFE AI INTERFACE follows a small set of principles:

### One workspace

AI, files, history and applications remain in one interface.

### One canonical Space

State is represented through UNISEFE CORE instead of introducing unrelated state systems for every feature.

### Permanent identity

The BYTE identifies the node.

The VALUE may change without replacing the identity.

### Visible persistence

User files remain normal files.

### Local before remote

The interface should remain useful even when much of the workspace is local.

### AI is replaceable

The intelligence provider is a component, not the application itself.

### Explicit authority

Operations that affect files or local applications are bounded by explicit permissions.

### Minimal infrastructure

A single HTML file can contain the core interface and runtime.

---

# Project direction

UNISEFE AI INTERFACE is intended to become a general workspace in which AI can work directly with:

```text
documents
code
HTML applications
projects
files
history
tools
connectors
UNISEFE-native applications
```

without fragmenting the user experience into separate tools.

The long-term direction is simple:

> **one interface, one Space, many capabilities.**

---

## Experimental status

This repository represents active experimental development.

Interfaces, connector contracts and browser integration may change between alpha versions.

Use test workspaces when experimenting with write operations.

---

# UNISEFE

```text
AI is not the workspace.

The workspace remains yours.

UNISEFE AI is the interface between
your files,
your applications,
your history,
your tools,
and intelligence.
```

**UNISEFE AI INTERFACE · Alpha**
