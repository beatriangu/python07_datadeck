🧭 MAP.md — Python Module 07 · DataDeck 🃏

OOP · ABC · Polimorfismo · Herencia múltiple · Patrones · flake8

Este documento describe la arquitectura del módulo DataDeck.
Aunque utiliza la metáfora de un juego de cartas, su propósito real es demostrar diseño orientado a contratos, extensibilidad y bajo acoplamiento.

🌱 Idea central

El sistema evoluciona desde:

❌ Diferenciar comportamientos mediante if / isinstance
a
✅ Delegar comportamiento a través de un contrato común (Card)

Principio rector

El motor depende de interfaces, no de implementaciones.

Las subclases encapsulan su propio comportamiento.

Añadir nuevas cartas no requiere modificar el motor.

Esto cumple el principio Open/Closed.

🧩 Arquitectura del sistema
Relación principal

Deck contiene cartas → composición

CreatureCard, SpellCard, ArtifactCard extienden Card → herencia

🎯 Diagrama UML simplificado
                +----------------+
                |     Deck       |
                +----------------+
                | - _cards:list  |
                +----------------+
                | +add_card()    |
                | +draw_card()   |
                | +shuffle()     |
                +--------+-------+
                         |
                         | contains
                         v
                +----------------------+
                | <<abstract>> Card    |
                +----------------------+
                | - name               |
                | - cost               |
                | - rarity             |
                +----------------------+
                | +play()              |
                | +is_playable()       |
                | +get_card_info()     |
                +----------+-----------+
                           ^
            ---------------|-------------------
            |              |                  |
+----------------+  +----------------+  +----------------+
| CreatureCard   |  | SpellCard      |  | ArtifactCard   |
+----------------+  +----------------+  +----------------+
| - attack       |  | - spell_type   |  | - durability   |
| - health       |  |                |  |                |
+----------------+  +----------------+  +----------------+

🟢 ex0 — Card Foundation
Objetivo

Definir el contrato base (Card) mediante una Abstract Base Class.

Decisiones clave

play() es abstracto para forzar implementación.

Card define comportamiento común, no implementación.

Se previenen errores en tiempo de instanciación.

🟡 ex1 — Deck Builder
Objetivo

Gestionar múltiples tipos de carta sin condicionales por tipo.

Diseño

Deck almacena list[Card].

El método play() se ejecuta de forma polimórfica.

El motor no conoce la clase concreta.

Polimorfismo real:

card = deck.draw_card()
card.play(game_state)

🟠 ex2 — Ability Layer (Herencia múltiple controlada)
Objetivo

Separar capacidades en interfaces independientes.

Interfaces:

Combatable

Magical

Representan capacidades, no identidad.

EliteCard
class EliteCard(Card, Combatable, Magical)


Permite componer comportamiento sin crear clases monolíticas.

Polimorfismo por capacidad

El sistema puede depender de:

Card

Combatable

Magical

Sin conocer la clase concreta.

🟣 ex3 — Patrones de diseño
Factory Pattern

Centraliza la creación de cartas.
Reduce acoplamiento y mejora escalabilidad.

Strategy Pattern

Permite modificar el comportamiento del motor mediante inyección de estrategia.

El motor no cambia.
Solo cambia el objeto estrategia.

🔴 ex4 — Extensibilidad

Se añade un nuevo contrato:

Rankable

Permite introducir un sistema de torneos sin modificar módulos anteriores.

Demuestra arquitectura abierta y desacoplada.

🧠 Design Trade-offs
1️⃣ ABC vs duck typing

Decisión: usar Abstract Base Classes.

Ventaja:

Contrato explícito

Errores detectados antes

Mayor claridad estructural

Trade-off:

Mayor rigidez inicial

Más código declarativo

2️⃣ Herencia múltiple vs composición pura

Decisión: usar herencia múltiple para capacidades.

Ventaja:

Modela habilidades como contratos formales

Permite polimorfismo por interfaz

Trade-off:

Riesgo de complejidad si se abusa

Necesidad de mantener jerarquía clara

3️⃣ Patrones vs simplicidad

Decisión: aplicar Factory y Strategy.

Ventaja:

Bajo acoplamiento

Configuración flexible

Escalabilidad

Trade-off:

Mayor abstracción

Más capas para entender al inicio

🧠 Conceptos practicados

Programación contra interfaces

Separación de responsabilidades

Bajo acoplamiento

Principios SOLID

Polimorfismo real

Extensibilidad sin modificación

🧪 Estándares de calidad

Python 3.10+

Tipado explícito

flake8 limpio

Sin condicionales por tipo

Ejecución modular:

python3 -m exX.main

📌 Resumen ejecutivo

DataDeck demuestra cómo diseñar un sistema extensible basado en contratos formales.
El motor depende de interfaces, no de implementaciones concretas.
La arquitectura permite añadir nuevas capacidades y comportamientos sin modificar el núcleo del sistema.

