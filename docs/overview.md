# Messadock – Dock áttekintés

A Messadock Sandor személyes Dock rendszere, amely a Messa AI-ra épül.  
Ez a „személyes lakás” réteg a Messa rendszerben: itt él a felhasználó saját világa, projektjei, dokumentumai és eszközei.

A Dock felett helyezkedik el a BuildUnion „város” réteg, de ennek dokumentációja külön fájlban szerepel.  
Ebben a dokumentumban **kizárólag a Dockra** koncentrálunk.

---

## 1. Szerepe a Messa rendszerben

A Dock fő feladatai:

- központi **belépési felület** a Messa világába,
- a felhasználó **személyes asszisztensének** (Messa) elsődleges tere,
- a saját projektek, fájlok, beszélgetések és média rendezett kezelése,
- hosszú távú, **Personal Continuum** jellegű történet fenntartása (élettörténet, döntések, jegyzetek, napló).

Röviden: a Dock az a hely, ahol a felhasználó a saját életével és projektjeivel dolgozik,  
és Messa ebben a térben segít neki.

---

## 2. Fő elemek (terv)

### 2.1 Lobby & Orb

A **Lobby** a Dock belépőképernyője.

Fő elemei:

- **Messa Orb**
  - kör alakú, központi elem, amelyen keresztül a felhasználó Messa-hoz fordul;
  - szöveges és hang alapú interakció indulhat rajta keresztül;
  - vizuálisan is visszajelzi a rendszer állapotát (gondolkodik, tölt, figyel, stb.).

- **BuildUnion kapszula-gomb** (az Orb felett)
  - egy külön gomb / kapszula, amely a „város” réteghez (BuildUnion) vezet;
  - a Dock szintjéről nyit át a közösségi / városi térbe;
  - jelen dokumentumban csak hivatkozásként szerepel, a részletes leírása a BuildUnion dokumentációban lesz.

- **TEXT / VOICE módok** (az Orb alatt)
  - két külön gomb:
    - **TEXT** – szöveges chat Messával;
    - **VOICE** – hangalapú kapcsolat (felvétel + visszajátszás / TTS).
  - ezek a gombok **gyors, vendég jellegű** kommunikációt biztosítanak,
    a mélyebb munkát a Dock Workspace végzi.

A Lobby célja: **gyors kapcsolat** a Messával, minimális zavaró elemmel, mobilon görgetés nélkül.

---

### 2.2 Dock Workspace

A **Dock Workspace** a tényleges munkafelület.

Itt jelennek meg többek között:

- projektek,
- dokumentumok,
- beszélgetések,
- média elemek (pl. Messadock Media),
- Personal Continuum jellegű idővonal / történet.

Fő jellemzők (terv):

- mobilra optimalizált nézet,
- chat + hang + média integráció,
- Messa aktív támogatása a feladatok szervezésében,
- kapcsolat a BuildUnionnal (pl. projektet ki lehet „emelni” a városi térbe).

---

### 2.3 Messadock Media (terv)

A **Messadock Media** a Dock média-rétege.

Feladata:

- zene és háttérmédiák kezelése,
- hívás alatti lejátszás (pl. koncentrációs zene),
- vizuális kísérőelemek (pl. háttéranimációk),
- a felhasználó saját fájljainak (mp3/mp4 stb.) integrálása – későbbi fázisban.

A Media modul önálló dokumentációt is kap a jövőben, de a Dock áttekintés szintjén fontos,  
hogy **külön rétegként** gondoljunk rá.

---

### 2.4 Personal Continuum (Dock szint)

A Personal Continuum a felhasználó hosszú távú történetét jelenti.

A Dock szintjén ez:

- események, döntések, projektek időbeli lánca,
- jegyzetek, naplók, fontos beszélgetések összefogása,
- összekötés a BuildUnion szintű közösségi / városi történésekkel.

Később ez külön dokumentációt kap („personal-continuum.md”),  
de a Dock áttekintésben már most rögzítjük, hogy ez kiemelt funkció.

---

## 3. Tervezett repo struktúra (Dock)

A Messadock repóban a következő fő mappák kialakítása a cél:

- `docs/` – dokumentáció, UX-leírások, architektúra
  - `overview.md` – ez a dokumentum (Dock áttekintés)
  - `architecture.md` – technikai / logikai architektúra (később)
  - `ux-lobby-orb.md` – Lobby & Orb részletes UX (később)
  - `personal-continuum.md` – Personal Continuum doksi (később)

- `src/` – a Dock alkalmazás forráskódja
  - később ide kerülnek a konkrét képernyők, komponensek, logika.

A mostani dokumentum első lépésként a Dock **koncepcionális** szintjét rögzíti.  
A részletes technikai leírás (`docs/architecture.md`) egy következő lépés lesz.

---

## 4. Jelenlegi állapot

- Messadock GitHub repo létrehozva (`messahq/Messadock`).
- ChatGPT–GitHub integráció engedélyezve a repóra.
- Alap README és első Dock dokumentáció (`docs/overview.md`) elkészült.
- Következő lépés: részletes Dock architektúra (`docs/architecture.md`) megtervezése.
