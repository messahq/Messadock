# BLOCK-02 – DOCK VOICE PIPELINE – V1

## Áttekintés
Ez a blokk a Messa voice pipeline első verzióját írja le. 
A cél: a mikrofonból érkező hang → Whisper transzkripció → GPT-4 Mini válasz → eredmény megjelenítése a VoiceTest oldalon.

A blokk **státusza**: ✅ KÉSZ, VALIDÁLT, STABIL  
Tesztoldal: `/VoiceTest` (külön sandbox, nem része a Dock főmenünek).

## Pipeline lépések

1. Mikrofon felvétel (browser / hook)
2. Hang blob → base64 konverzió
3. Kérés a backend felé:
   - Endpoint: `functions/transcribeAudio`
   - Technológia: OpenAI Whisper + GPT-4 Mini
4. Whisper:
   - Input: audio (base64)
   - Output: szöveges transzkripció (felhasználó üzenete)
5. GPT-4 Mini:
   - Input: transzkripció (user message)
   - Output: Messa válasza (assistant reply)
6. VoiceTest UI:
   - „Click to start recording” gomb
   - „Your Message” mező: a transzkripció
   - „Messa’s Reply” mező: a GPT-4 Mini válasza
   - „Clear Results” gomb
   - Alul pipeline felirat: „Microphone → Recording → Whisper API → GPT-4 Mini → Response”

## Fájlok (implementáció jelenlegi helye – nem GitHubon)

- `functions/transcribeAudio.js` – Whisper + GPT-4 Mini backend hívás
- `components/hooks/useVoiceRecording.js` – hangfelvétel kezelése a böngészőben
- `pages/VoiceTest.js` – VoiceTest sandbox UI

Ezek a fájlok jelenleg a BuildUnion / Base44 környezetben futnak. 
A GitHub repó most **csak a blokk specifikációját** tárolja, nem a teljes kódot.

## Validáció

- A VoiceTest oldalon tesztelve:
  - A felvétel elindul
  - Pontos Whisper transzkripció érkezik
  - GPT-4 Mini releváns választ ad
  - Az UI helyesen megjeleníti a „Your Message” és „Messa’s Reply” blokkokat

Ezzel a blokk lezártnak tekinthető, és készen áll a Dock Orb voice integráció (következő blokk) előkészítésére.
