 # Messadock

Messadock Sandor személyes Dock rendszere, amely a Messa AI-ra épül.  
Ez a repo tartalmazza a Dock app logikáját, UX-terveit és a BuildUnionnal való kapcsolódást.

---

## Cél

* Egy központi **Dock felület**, ahol:
  * a Messa személyes asszisztens és „főnök”,
  * a felhasználó egy helyen éri el a saját projektjeit, dokumentumait és eszközeit,
  * a rendszer hosszú távon **Personal Continuum** jellegű folyamatos történetet tart fenn.

* Integráció a **BuildUnion** rendszerrel:
  * a Dock a „személyes lakás”,  
  * a BuildUnion a „város / közösségi tér”.

---

## Fő elemek (terv)

1. **Lobby & Orb**
   - Belépési pont a Dockba.
   - Középen az Orb, felette BuildUnion kapszula-gomb, alatta TEXT / VOICE módok.
   - Mobil-első, görgetés nélküli kezdőképernyő.

2. **Dock Workspace**
   - A tényleges munkafelület, chat + hang + média.
   - Itt jelennek meg:
     - projektek,
     - dokumentumok,
     - media player (Messa Media),
     - jövőbeli Personal Continuum  nézetek.

3. **Messa Media**
   - Beépített media player (zene / háttérlejátszás).
   - Később: Media Library, saját fájlok (mp3/mp4), hívás alatti lejátszás.

4. **Personal Continuum (későbbi fázis)**
   - Hosszú távú, idővonal-szerű nézet arról, hogyan fejlődik a felhasználó világa.
   - Cél: mindenkit Pro / Premium szintre húzni valódi értékteremtéssel.

---

## Repo felépítés (terv)

A következő mappák fokozatosan fognak megjelenni:

- `docs/` – dokumentáció, UX-leírások, architektúra
  - `overview.md` – összkép a Messadock rendszerről
  - `architecture.md` – technikai / logikai architektúra
  - `ux-lobby.md` – Lobby & Orb végleges UX
- `src/` – a Dock alkalmazás forráskódja
  - pl. `src/app/...`, `src/components/...`

Ezek a fájlok most még csak tervként szerepelnek, de a ChatGPT–GitHub integráció számára már kijelölik a struktúrát.

---

## Kapcsolódás a BuildUnion  repohoz

Ez a Messadock repo **párban dolgozik** a `BuildUnion` repóval:

- Messadock = személyes Dock / saját világ
- BuildUnion = város / közösség / közös projektek

A két repo együtt alkotja a teljes rendszert, amelyet a Messa AI koordinál.

---

## Állapot

**2025-12-xx – első GitHub verzió**

- GitHub repo létrehozva (`messahq/Messadock`)
- ChatGPT Codex Connector engedélyezve erre a repóra
- Alap README dokumentáció elkészítve az indexeléshez

A következő lépés: `docs/` mappa létrehozása és részletesebb dokumentáció hozzáadása.

