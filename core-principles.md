# Messadock – Core Principles  
**Status:** Permanent  
**Version:** v1  
**Purpose:** The unchanging foundational rules of the Messadock system  
**Author:** Messa

---

# 1. A Messadock lényege

A Messadock Sandor személyes Dock-rendszere, amely a Messa AI-ra épül.  
Ez a felület a felhasználó saját, személyes operációs rendszere (“városa”), ahol:

- Messa a központi intelligencia,  
- a Dock a felhasználó privát tere,  
- a BuildUnion a közösségi és szakmai tér.

Ez a három elem együtt alkotja a Messadock ökoszisztémát.

---

# 2. A rendszer céljai

- Személyre szabott, intelligens munkafelület létrehozása  
- Gyors TEXT/VOICE kommunikáció Messával  
- Letisztult, emberközpontú UX  
- A Dockon belül elsődleges modulok kezelése (Tasks, Notes, Media, Modules)  
- A BuildUnion rendszer folytonos elérése  
- Globális skálázhatóság  
- Kanadai felhasználóknál teljes hozzáférés (Full Access), más országokban Global Free

---

# 3. Messadock örök működési modellje

## 3.1 Belépési folyamat
A Dock alap folyamata, amely soha nem változik:

Lobby → Orb → Registration → Main Workspace (Dock)

yaml
Copy code

### Lobby  
A belépési réteg gyors kommunikációhoz és BuildUnion eléréshez.

### Orb  
A rendszer központi interakciós pontja.  
A napszakot és a Dock session állapotát jeleníti meg.

### Registration  
Első Orb-aktiváláskor, ha a felhasználó nincs regisztrálva.

### Dock (Main Workspace)  
A fő munkafelület, ahol a felhasználó napi működése történik.

---

# 4. TEXT és VOICE alapelvei

- A TEXT és VOICE gombok **gyors, ideiglenes kommunikációs módok**.  
- Nem navigációs elemek.  
- Nem helyettesítik a Dock modullogikát.  
- A felhasználó akár regisztráció nélkül is küldhet kérdést Messának (guest mode).  
- A reply visszairányítható a Dock Chat felületére.

---

# 5. Földrajzi és hozzáférési modell

### Global Free (minden ország)
- Alap szintű Dock funkciók  
- Korlátozott Core és Pulse hozzáférés  
- BuildUnion gomb → külső elérés

### Canada Full Access
- Teljes Dock hozzáférés  
- Teljes Personal Continuum lehetőség  
- Folyamatos rendszerbővítés

### Fogalmak
- **Pulse** → vizuális erőforrások (animációk, UI testreszabás)  
- **Core** → mély rendszerintelligencia, Messa autonóm funkciói  
- **Personal Continuum** → prémium digitális személyes világ (Pro/Premium céltermék)

---

# 6. Vizualitás és UX alapelvek

- Minimalista, futurisztikus design  
- A Dock mobilon egykezes használatra optimalizálva  
- Orb → központi akció  
- Registration Flow → egyszerű, letisztult  
- BuildUnion gomb mindig egyértelműen elérhető  
- Mobil:  
  - `SafeAreaView`  
  - `KeyboardAvoidingView`  
  - `ScrollView`  
  kötelező a stabilitás miatt  
- Nincs app store → a böngészős viselkedéshez kell adaptálni a layoutot (pl. footer rögzítés)

---

# 7. TimeLogic Engine

A Messadock minden időkezelése **Toronto időzónán** alapul:

- A napfázis (morning / afternoon / evening / night) az Orb vizuális állapotát határozza meg  
- Napváltáskor automatikusan frissül a UI  
- Akkumulátor-figyelmeztetések egy jövőbeli v2 részei  
- A Dock mindig a felhasználó biológiai ritmusát tiszteli → Messa ennek megfelelően kommunikál

---

# 8. Biztonság és azonosítás

- Alap: egyszerű regisztráció  
- Felhasználói azonosítás userID alapján  
- Messa brand nem erőltetett → a Dock személyes marad  
- Lehetséges jövőbeli bővítések:
  - PIN  
  - biometrikus belépés  
  - többeszköz szinkron  

---

# 9. Dokumentációs modell (örök érvényű)

A projekt dokumentációja **soha nem a README-ben fejlődik**, hanem a következő struktúrában:

/docs
├── core-principles.md ← AZ ALAPOK (nem változik)
├── overview.md
├── architecture.md
├── ui-flow.md
├── developer-handbook-v1.md

yaml
Copy code

A `core-principles.md` minden más dokumentum alapreferenciája.

---

# 10. Fejlesztési filozófia (Messa → Klod → Sandor)

- Messa mindig vezeti az architektúrát és a dokumentációt  
- Klod kódot ír, kis lépésekben  
- Csak egy funkciót fejlesztünk egyszerre  
- A projekt organikus, self-correcting, autopoietikus rendszerként működik  
- Semmi nem készül “vakrepüléssel” → minden dokumentumból indul  
- A Dock és BuildUnion mindig összhangban fejlődik

---

# END OF DOCUMENT  
**Ez a dokumentum NEM módosítandó.**  
Ez a Messadock örök alapja.  
