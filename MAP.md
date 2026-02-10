# 🧠 MAP.md — Learning Map · Python Module 07 (DataDeck)
**OOP · Herencia · Polimorfismo · Diseño extensible · flake8**

## 🎯 Visión global del módulo
Este módulo construye un mini-sistema de cartas tipo TCG para practicar
**programación orientada a objetos** con foco en:

- **Herencia**: clases base y subclases especializadas.
- **Polimorfismo**: misma interfaz, comportamientos distintos.
- **Diseño extensible**: añadir nuevas cartas sin romper el sistema.
- **Disciplina de estilo**: flake8, estructura limpia, ejecución separada.

> Idea central (defendible):
> **La misma llamada (`card.play(...)`) funciona para todas las cartas,**
> y cada tipo decide internamente qué hacer.

---

## 🧩 Progresión por ejercicios
### ex0 — `CreatureCard` (primera subclase real)
**Meta**
- Modelar una carta concreta con atributos propios (ej: ataque/vida)
- Mantener interfaz común (métodos compartidos con otras cartas)

**Aprendizaje clave**
- Una subclase **extiende** (añade cosas) sin romper el contrato.
- Un objeto “se comporta como una carta”, aunque sea una criatura.

---

### ex1 — `Deck` + tipos variados (polimorfismo en acción)
**Meta**
- Crear un mazo que almacene cartas de distintos tipos:
  - criatura (`CreatureCard`)
  - hechizo (`SpellCard`)
  - artefacto (`ArtifactCard`)
- Demostrar que el mazo opera con todas igual:
  - `add_card(card)`
  - `draw_card()`
  - `get_deck_stats()`
- Ejecutar una demo donde:
  - robas una carta
  - imprimes info
  - la juegas con `card.play(game_state)`

**Aprendizaje clave**
- El mazo no necesita saber “qué tipo” es cada carta.
- El comportamiento se resuelve por **dynamic dispatch**:
  - misma llamada
  - método distinto según la clase real

---

## 🧱 Arquitectura mental (modelo del sistema)
### Entidades
- **Card (concepto base)**  
  Interfaz común: `get_card_info()` y `play(game_state)`
- **Cartas concretas**
  - `CreatureCard`: ataque/vida y lógica propia
  - `SpellCard`: spell_type, daño/efecto
  - `ArtifactCard`: efecto permanente, durabilidad
- **Deck**
  - Contiene una colección de cartas
  - Implementa operaciones de mazo (añadir, robar, estadísticas)

### Flujo de ejecución (demo)
1. Crear `Deck`
2. Crear cartas distintas
3. `deck.add_card(...)` para todas
4. Repetir:
   - `card = deck.draw_card()`
   - `info = card.get_card_info()`
   - `card.play(game_state)`

---

## 🔑 Conceptos que debes poder defender
### 1) Herencia vs composición
- Herencia: “CreatureCard ES una Card” (especializa comportamiento)
- Composición: el Deck TIENE cartas (colección de objetos)

### 2) Polimorfismo (sin condicionales)
✅ Correcto:
- `card.play(...)`  
- cada subclase sobrescribe `play()` con su lógica

❌ Evitar:
- `if info["type"] == "Creature": ...`
- `isinstance(card, CreatureCard)`

### 3) Contrato / interfaz común
Aunque las cartas tengan atributos distintos, todas cumplen:
- `get_card_info()` devuelve un dict consistente
- `play(game_state)` devuelve un resultado interpretable

---

## ✅ Checklist de calidad (antes de entregar)
- [ ] `flake8` pasa sin E501 / W391
- [ ] `main()` solo hace demo (no lógica pesada)
- [ ] Clases con **una responsabilidad**
- [ ] `Deck` no conoce detalles internos de cada carta
- [ ] Salida de consola clara y repetible

---

## ⚠️ Errores típicos (y cómo evitarlos)
- **E501 líneas largas**  
  - dividir prints o strings con paréntesis
- **W391 línea en blanco al final**  
  - eliminar salto extra al final del archivo
- **Deck con lógica por tipo**  
  - si empiezas a meter `if card_type`, estás rompiendo el objetivo
- **Cambiar el diseño al añadir una carta**  
  - ideal: añadir `NewCard` y que funcione sin tocar `Deck`

---

## 🗣️ Mini-guion de defensa (30–60s)
“En este módulo practico OOP creando un sistema de cartas.
El Deck guarda objetos de distintos tipos, pero los trata con la misma interfaz.
La clave es el polimorfismo: siempre llamo a `card.play(game_state)` y cada
subclase implementa su comportamiento sin condicionales en el mazo.
Así el sistema es extensible: puedo añadir nuevas cartas sin modificar el Deck.”

---

## 📌 Próximos pasos
- Añadir más tipos de carta manteniendo interfaz
- Aumentar validaciones (sin romper diseño)
- Mejorar estadísticas del mazo sin acoplarse a tipos concretos
