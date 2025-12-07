## Messadock Architecture

Ez a dokumentum a Messadock rendszer **magas szintű architektúráját** írja le.  
Célja, hogy a fejlesztők (Klod), a Messa-réteg és a jövőbeli együttműködők számára
egy egységes, áttekinthető szerkezetet adjon.

---

## 1. Rendszerkép – hol helyezkedik el a Messadock?

A Messadock a Messa-rendszer **„személyes dokk”** rétege:

- alatta: Messa AI, Core / Orchestrator réteg  
- felette: a felhasználó mindennapi munkafelülete (Dock UI)  
- oldalirányban: kapcsolódás a **BuildUnion** „város / közösség” réteghez

Logikailag így néz ki:

- **Messa Core** – intelligencia, döntés, hosszú távú memória  
- **Messadock** – személyes munkafelület, projektek, média, kommunikáció  
- **BuildUnion** – közösségek, csapatok, városi tér, közös projektek

A Messadock tehát a felhasználó „lakása”, ahonnan:

- eléri a saját eszközeit, dokumentumait,  
- kommunikál Messával (TEXT / VOICE),  
- kilát az „erkélyre” → BuildUnion világára.

---

## 2. Fő modulok (logikai bontás)

A Messadock architektúrája modulokból áll. A fő egységek:

### 2.1 Lobby & Orb

- **Belépési pont** a Dockba.
- Mobilon: teljes képernyős kezdőfelület, középen az **Orb**.
- Az Orb funkciói:
  - Messával való azonnali interakció (TEXT / VOICE).
  - Dock állapotainak rövid összegzése („open tasks”, media, meetingek).
  - Átvezetés a BuildUnion felé (külön kapszula-gomb).

**Technikai szerep:**

- eseményeket indít (voice start/stop, chat session, navigation)  
- státusz jelzések (online, töltés, háttérműveletek)  
- kommunikál a Messa Core felé → API / messaging réteg

### 2.2 Dock Workspace

Ez a tényleges **munkafelület**, ahol:

- chat + hang + média + projektek jelennek meg,
- a felhasználó hosszabb folyamatokat visz végig.

Fő al-modulok:

1. **Chat & Timeline**
   - Messa válaszai, múltbeli beszélgetések
   - „Personal Continuum” jellegű folytonos történet
2. **Task / Project View**
   - feladatok, jegyzetek, mini-projektek
   - kapcsolódó dokumentumok és media
3. **Media Panel**
   - Messadock Media Player (zene, hang, háttérlejátszás)
   - Media Library (helyi és online források, későbbi fázisban)
4. **System State & Notifications**
   - státusz üzenetek: szinkronizálás, töltés, háttérfolyamatok

### 2.3 Settings & Profiles (későbbi modul)

- személyes beállítások (nyelv, értesítések, megjelenés – Pulse)  
- Messa személyre szabása (stílus, hangvétel, asszisztens-módok)  
- biztonsági réteg (PIN / biometria, eszköz-jogosultságok)

---

## 3. Adat- és vezérlési áramlás (egyszerűsített modell)

A Messadock működésének logikája:

1. **Felhasználói input**
   - Lobby Orb: TEXT / VOICE indítás
   - Dock Workspace: chat üzenet, gomb, navigáció, media esemény
2. **Dock Controller réteg**
   - normalizálja az inputot
   - eldönti, hogy:
     - Messa Core felé megy (AI feldolgozás),
     - helyi Dock-funkció (pl. media vezérlés, navigáció),
     - BuildUnion felé átadandó kérés (projekt / közösségi tárgyú).
3. **Messa Core válasz**
   - nyers AI válasz (szöveg, struktúrált JSON, action-sugallat)
4. **Dock Interpreter**
   - a nyers választ **Dock-szintű műveletté** alakítja:
     - üzenet megjelenítés
     - task létrehozás / módosítás
     - media lejátszás indítása
     - BuildUnion hívás kezdeményezése
5. **Render / UI**
   - vizuális frissítés (chat, listák, player, státusz)

Ez a logika biztosítja, hogy a Messadock **nem csak chat**, hanem egy
folyamatos, állapot-alapú munkafelület.

---

## 4. Állapotkezelés (State)

A Dockban három fő állapottípust különböztetünk meg:

1. **UI State**
   - melyik képernyőn vagyunk (Lobby, Workspace, Media, stb.)
   - aktív panelek, nyitott modálok
2. **Session State**
   - aktuális beszélgetés Messával
   - ideiglenes változók (aktuális projekt, fókusz-téma)
3. **Persistent State**
   - mentett beállítások, projektek, jegyzetek
   - hivatkozások BuildUnion objektumokra
   - media-lejátszási előzmények (később)

Az architektúra célja, hogy:

- **UI State** gyorsan reagáljon és frissüljön,  
- **Session State** folyamatos és Messa-barát legyen,  
- **Persistent State** jól szinkronizálható legyen más eszközök / rétegek felé.

---

## 5. Integráció a BuildUnionnal

A Messadock és a BuildUnion kapcsolata:

- Messadock = „lakás” / személyes tér  
- BuildUnion = „város” / közösségi tér

Kapcsolódási pontok (terv):

1. **Project Link**
   - Dock-ban létrehozott projekt → hivatkozás egy BuildUnion-projektre
   - kétirányú kommunikáció lehetséges később
2. **City View Shortcut**
   - Dockból egy gomb / kapszula átvált BuildUnion nézetre
3. **Shared Context**
   - Messa tudja, hogy egy kérdés:
     - személyes (Dock),
     - vagy közösségi / szervezeti (BuildUnion) kontextushoz tartozik.

Ez logikailag úgy néz ki, hogy a Messadock architektúrája:

- önmagában is teljes értékű személyes workspace,
- de minden elemében kész a **BuildUnion-irányú export / linkelés** lehetőségére.

---

## 6. Jövőbeli bővítések (terv)

Az architektúra úgy van tervezve, hogy:

- könnyen bővíthető legyen további modulokkal:
  - Meeting / Room integráció
  - File-kezelés (saját tárhely, Drive integráció, stb.)
  - Pulse / vizuális témák dinamikus kezelése
- kompatibilis legyen több klienssel:
  - mobil / tablet
  - későbbi desktop / web kliens

A Messadock hosszú távú célja, hogy:

- a felhasználónak **egy helyen** legyen a személyes AI-központja,  
- a Messa-rendszerrel és a BuildUnionnal szorosan, mégis átlátható módon integrálva.

---

## 7. Aktuális státusz

- README és `docs/overview.md` elkészítve  
- `docs/architecture.md` – jelen dokumentum – kijelöli a Dock logikai szerkezetét  
- Következő lépés későbbi fázisban:
  - részletesebb technikai specifikáció (API-k, adatmodellek)
  - UX-flowk és képernyő-tervek dokumentálása
