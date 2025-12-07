# Messadock – Dock UI & Flow v1  
**Author:** Messa  
**Status:** Finalized  
**Purpose:** Stable development specification for Klod (Dock v1 implementation)

---

# 1. Overview

This document defines the **final v1 logic, UX flow and technical requirements** for the Messadock application.  
It ensures consistent behavior across mobile and desktop and provides a clear development roadmap for Klod.

The Dock is the **primary workspace**, while the **Lobby** is a controlled entry layer with quick messaging (TEXT/VOICE).

---

# 2. Core Concepts

### **Lobby**
Entry surface of Messadock, containing:
- ORB (state-driven)
- BuildUnion button (external URL)
- TEXT / VOICE quick-entry buttons

### **Dock**
The user’s main operating environment:
Tasks, Notes, Media, Profile, Settings, Modules, etc.

### **Orb**
Central stateful entry controller:
- OFF → BOOTING → ON
- Responds to time of day: morning / afternoon / evening / night
- Controls session logic

### **TEXT / VOICE**
Quick “guest mode” communication channels, not used for navigation.

---

# 3. State Model

```ts
interface DockState {
  isRegistered: boolean;
  isDockSessionActive: boolean;

  orbState: "off" | "booting" | "on";
  dayPhase: "morning" | "afternoon" | "evening" | "night";
}
4. High-Level Lifecycle
User opens Lobby

User sees:

ORB (center)

BuildUnion (capsule button above)

TEXT / VOICE (below)

ORB → first activation:

if not registered → Registration Card

if registered → Dock

After registration, Dock becomes the default environment

Next visits:

ORB restores Dock session if possible

5. Registration Flow (First Dock Entry)
Triggered when:

isRegistered = false

ORB tapped

Registration Card Requirements
Full-screen or modal overlay (fluid on mobile)

Fields:

Name

Email

Country

(Reserved fields for future: Status / Role)

Button: “Enter Dock”

Upon success:
ts
Copy code
isRegistered = true;
isDockSessionActive = true;
orbState = "on";
User is routed to Dock main interface.

6. TEXT & VOICE – Quick Mode Communication
Purpose:
Not navigation tools — instead:

quick questions

rapid messaging

works even before registration

Behavior:
TEXT button
Opens a bottom sheet / overlay chat input

Guest-mode allowed (before register)

If registered → forwarded to Dock Chat context

VOICE button
Starts voice pipeline:

Record audio

Whisper transcription

Route to Dock Chat

TTS reply (Lobby or Dock context)

7. Dock as the Main Workspace
After registration, Dock is the home base.

Modules (v1):
Dashboard / Home

Tasks

Notes

Media / Player

Profile

Settings

Modules (placeholders)

Navigation is internal within Dock (not from Lobby).

8. Mobile UI Requirements
Global
All important screens must use:

SafeAreaView

KeyboardAvoidingView

ScrollView for forms

predictable layout on iOS/Android

8.1 Registration Screen (Mobile)
Container layout:

markdown
Copy code
SafeAreaView
  KeyboardAvoidingView
    ScrollView
       RegistrationCard
CTA button always reachable.
Keyboard must NOT push UI into unreachable positions.

8.2 All Dock Screens (Mobile)
Use scroll-safe layouts

Footer must never overlap with CTA buttons

Media Player mini-bar must remain visible when active

9. Global Footer (Dock)
Rationale:
Prevents mobile UI jumping, improves stability.

Requirements:
Always visible on Dock screens

Unified spacing and padding

May contain:

quick nav hints

“Now Playing” mini media bar

home/back icon (optional)

Must cooperate with KeyboardAvoidingView.

10. BuildUnion Link (Lobby)
Requirements:
BuildUnion button in Lobby opens external URL

Not a Dock module

New tab on desktop

In-app browser or external browser on mobile

Configurable via environment variable.

11. Implementation Checklist for Klod
Orb
state machine + dayPhase

booting animation

session start/stop

Registration
mobile-friendly scroll layout

submit → save user → Dock redirect

TEXT/VOICE
implement quick modes

ensure transcription → Dock Chat routing

Dock
stable navigation

module placeholders

persistent session

Footer
global component

consistent placement on all screens

BuildUnion Button
external link handling

ensure no navigation conflict with Dock router

12. Future Expansions (not for v1)
Orb timezone visualization

Personal Continuum (Pro/Premium)

multi-device session restore

deeper Media background integration

BuildUnion ↔ Dock identity sync

END OF DOCUMENT
yaml
Copy code

---

### ✔️ **3. Commit üzenetnek írd be:**

**Title:**
Add Dock UI & Flow v1 specification

makefile
Copy code

**Description:**
Added ui-flow.md containing final Dock registration, Lobby, TEXT/VOICE, Orb, and mobile UX specifications. Ready for Klod implementation. ## Dock Registration Flow v1 — IMPLEMENTED

Status: Completed
Implementation: 2025-12
Developer: Klod
Architecture Reference:

core-principles.md

docs/developer-handbook-v1.md

### 1. Overview

A Dock Registration Flow v1 az első teljes, stabil regisztrációs folyamat a Messadock rendszerben.
Ez a flow biztosítja, hogy:

az új felhasználók egyszerűen, gyorsan létrehozzák a Dock-profiljukat

a rendszer megjegyzi a regisztrációt

a jövőben automatikusan a Dock főképernyőre navigál a felhasználó

a Lobby Orb viselkedése következetes a core logikával

Ez a verzió megfelel a Messadock stabil alapelveinek (core-principles).

### 2. User State Logic

A regisztráció állapotát a useUserStore kezeli (Zustand + AsyncStorage):

isRegistered: boolean

profile: { name, email?, country?, status? }

loadUser() – app indításakor beolvassa az állapotot

register(profile) – elmenti a felhasználót és aktiválja a Dockot

logout() – fejlesztői / debug funkció a profil törlésére

Storage key: @messadock_user

### 3. Flow Specification (Implemented)
Lobby Orb Tap
isRegistered === false → RegistrationScreen
isRegistered === true  → DockMain

RegistrationScreen

Mezők:

Name (kötelező)

Email (opcionális)

Country (opcionális)

Status/Role (opcionális)

Viselkedés:

“Enter Dock” gomb csak akkor aktív, ha Name ki van töltve

regisztrációkor a userStore menti az adatokat

sikeres mentés után: navigation.replace("DockMain")

Mobil stabilitás:

SafeAreaView

KeyboardAvoidingView

ScrollView

### 4. Navigation

A navigációs struktúra a következő logikával készült:

if (!isRegistered) {
  Screens: Lobby, Registration
} else {
  Screen: DockMain
}


Ez a core-principles dokumentumban meghatározott modell teljes implementációja:

Lobby → Orb → Registration → DockMain

### 5. Implementation Files

src/state/userStore.ts

src/screens/RegistrationScreen.tsx

src/navigation/index.tsx

src/screens/LobbyScreen.tsx (Orb tap logika)

### 6. Version Notes (v1)

Backend integráció NEM része (későbbi verzióban érkezik)

Personal Continuum logika később kapcsolódik

Kanada Full Access logika még nincs aktiválva

A flow jelen állapotában teljesen stabil és gyártásra kész
