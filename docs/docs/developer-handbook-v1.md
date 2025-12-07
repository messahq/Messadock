MESSADOCK – Developer Handbook v1

(GitHub-feltöltésre kész teljes dokumentum)

# Messadock – Developer Handbook v1
**Author:** Messa  
**Version:** v1  
**Status:** ACTIVE  
**Scope:** Dock system implementation guide for developers (Klod)

---

# 1. Introduction

Messadock is Sandor’s personal AI-driven Dock system built on top of the Messa architecture.  
This handbook provides practical development guidance, covering:

- system architecture  
- state logic  
- UI structure  
- registration flow  
- Orb behavior  
- Text/Voice pipeline  
- navigation rules  
- mobile requirements  
- external integration (BuildUnion)

This is the official v1 development reference.

---

# 2. System Overview

Messadock consists of:

1. **Lobby Layer** – Entry layer with Orb + quick messaging + BuildUnion button  
2. **Dock Layer** – Main workspace (Tasks, Notes, Media, Profile, Settings, Modules)  
3. **Services Layer** – Voice Engine, Text Processor, State Manager, Storage  
4. **Messa Core Layer** – AI logic, chat, reasoning engine  
5. **External Systems** – BuildUnion site, future APIs

---

# 3. Core Principles

### 3.1 Dock is the workspace  
All meaningful user actions happen in the Dock, not the Lobby.

### 3.2 Minimal entry friction  
The Orb handles session bootstrapping and user authentication.

### 3.3 Quick communication modes  
TEXT and VOICE are lightweight “guest mode” communication channels.

### 3.4 Mobile-first reliability  
KeyboardAvoidingView + SafeAreaView + ScrollView everywhere needed.

### 3.5 Modular structure  
Every module (Tasks, Notes, Media, etc.) should be isolated & scalable.

---

# 4. Project Folder Structure



/ (root)
├─ README.md
├─ package.json
├─ src/
│ ├─ components/
│ ├─ screens/
│ ├─ state/
│ ├─ services/
│ ├─ navigation/
│ ├─ hooks/
│ └─ utils/
└─ docs/
├─ overview.md
├─ architecture.md
├─ ui-flow.md
└─ developer-handbook-v1.md


> NOTE: Actual folder names may vary depending on Klod’s implementation.  
> This is the recommended standard structure.

---

# 5. State Architecture

```ts
interface DockState {
  isRegistered: boolean;
  isDockSessionActive: boolean;
  orbState: "off" | "booting" | "on";
  dayPhase: "morning" | "afternoon" | "evening" | "night";
}

State handlers include:

Registration Manager

Session Manager

Orb State Machine

Media Player State

Chat + Voice Pipeline State

All state should be stored in:

in-memory store (Zustand or custom)

persisted store (AsyncStorage) after registration

6. Orb Logic Specification

The Orb has three states:

off → booting → on

Behavior:

OFF → first touch → BOOTING

BOOTING → check registration

not registered → show Registration Card

registered → enter Dock

ON → Dock session active

Visual states:

morning (sun)

afternoon (neutral sun)

evening (warm tone)

night (moon)

ORB must always reflect Toronto time (America/Toronto).

7. Registration Flow (Developer Version)
Trigger:

User taps Orb for the first time

isRegistered is false

Requirements:

Full-screen overlay

Mobile-optimized layout

Fields:

name

email

country

optional: role/status (future)

On success:
isRegistered = true
isDockSessionActive = true
orbState = "on"


User is routed to Dock Home.

8. Text Mode (Quick Chat)
Behavior:

Opens a bottom-sheet style minimal chat

Sends message to Messa

If user is registered → message also appears in Dock Chat

If unregistered → treat as guest-mode

Developer notes:

Use lightweight UI, no heavy navigation.

9. Voice Mode (Pipeline)
Steps:

Start recording

Whisper transcription

Send text to Messa

Receive AI response

Text-to-Speech playback

Log message in Dock Chat context (if registered)

Developer notes:

Ensure pipeline does not break on network variance

Must allow cancel/cutoff of playback

Background mode (future version)

10. Dock Navigation Rules
Modules:

Dashboard

Tasks

Notes

Media

Profile

Settings

Modules (placeholders)

Navigation requirements:

No navigation from Lobby except Orb

All module routing handled inside Dock

Consider using a tab navigator or custom bottom nav with Footer integration

11. Footer Specification
Requirements:

Always visible in Dock

Must not overlap with soft keyboard

Can contain:

Now Playing (Media mini-bar)

Simple navigation icons

Status indicators

Footer is NOT shown on Lobby.

12. Media Engine Notes
Current expected behavior:

Play/Pause must persist across navigation

Audio should continue during screen transitions

Background audio (future v2)

Voice playback should interrupt music automatically

State requirements:
mediaState = {
  isPlaying: boolean,
  track: object | null,
  progress: number
}

13. BuildUnion Integration
Requirements:

Button located ABOVE the Orb in Lobby

Opens an external URL

New tab (desktop)

External browser or in-app browser (mobile)

Developer note:

This is NOT a Dock module.

14. Error Handling & Stability Guidelines
Orb must never freeze

If state fails, reset to off.

Voice must fail gracefully

If transcription fails, show retry.

Registration may not block UI

If submit fails:

show error toast

remain on registration screen

allow retry

Media must recover after reload

Persist last track if possible.

15. Developer Checklist (For Klod)
MUST implement:

Orb State Machine

Registration Flow

TEXT Mode

VOICE Mode

Dock navigation

Footer

Safe mobile layouts

BuildUnion external opening

OPTIONAL (v2+):

Background audio

Animated Orb transitions

Personal Continuum UI hooks

16. Final Notes

This handbook is the official Dock v1 implementation guide.
All future updates should be versioned:

developer-handbook-v2.md
developer-handbook-v3.md
