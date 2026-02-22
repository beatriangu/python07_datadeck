🃏 DataDeck — Python Module 07
Advanced Object-Oriented Architecture in Python

OOP · Abstract Base Classes · Multiple Inheritance · Polymorphism · Design Patterns · flake8

DataDeck is a modular, Trading Card Game–inspired architecture designed to practice clean, extensible, and defendable object-oriented design in Python.

This project is not about building a game.
It is about designing an architecture that can evolve without breaking.

🎯 Core Philosophy

Same interface. Different behavior. No conditionals. No isinstance().

The system is built around a single principle:

The engine depends on abstractions, not implementations.

Behavior is delegated to objects.

Extensibility does not require modifying existing code.

🧠 Architectural Goals

Design a system where:

The engine depends on interfaces, not concrete classes

New card types can be introduced without engine modification

Behavior is encapsulated within objects

The architecture respects SOLID principles

Code remains flake8-clean and evaluation-ready

📚 Concepts Demonstrated

This module implements:

✅ Open/Closed Principle

✅ Low coupling & high cohesion

✅ Interface-driven design

✅ Runtime polymorphism

✅ Strategy Pattern

✅ Abstract Factory Pattern

✅ Controlled multiple inheritance

🧩 Learning Outcomes

After completing this module, I can:

Define explicit contracts using Abstract Base Classes (ABC)

Enforce behavior consistency across subclasses

Demonstrate true runtime polymorphism (card.play(...))

Combine capabilities using multiple inheritance

Apply Strategy and Factory patterns correctly

Structure a Python project as a modular package

Deliver flake8-compliant, production-ready code

⚙️ Project Constraints

Python 3.10+

Standard library only

Fully flake8 compliant

Executable modular structure

Run exercises from the repository root:

python3 -m ex0.main
python3 -m ex1.main
python3 -m ex2.main
python3 -m ex3.main
python3 -m ex4.main
📦 Repository Structure
python07_datadeck/
├── README.md
├── MAP.md
├── ex0/  # ABC foundation
├── ex1/  # Polymorphism in collections
├── ex2/  # Multiple inheritance (interfaces)
├── ex3/  # Strategy + Factory
└── ex4/  # Ranking & orchestration

Each exercise is isolated, modular, and executable.

🧩 Exercise Breakdown
🟢 ex0 — Card Foundation

Abstract Base Class + First Concrete Implementation

Goal

Create a universal contract for all card types.

Design

Card (ABC)

play(game_state) → abstract

get_card_info() → shared implementation

is_playable() → shared validation logic

CreatureCard

Adds attack & health

Implements play()

Extends behavior without breaking the contract

Demonstrates

Contracts prevent incomplete implementations

Subclasses define behavior

The system depends on abstraction

Run:

python3 -m ex0.main
🟡 ex1 — Deck Builder

Polymorphism in Action

Goal

Store multiple card types in the same collection and treat them uniformly.

card = deck.draw_card()
card.play(game_state)

The deck does not know:

If it’s a creature

If it’s a spell

If it’s an artifact

Only the contract matters.

Demonstrates

Runtime polymorphism

Elimination of conditional branching

Distributed responsibility

Run:

python3 -m ex1.main
🔵 ex2 — Ability Layer

Multiple Interfaces & Capability Composition

Problem

Some cards can:

Attack

Defend

Cast spells

Channel mana

Solution

Separate capabilities into independent interfaces:

Combatable

Magical

class EliteCard(Card, Combatable, Magical)

These represent capabilities, not identity.

Demonstrates

Intentional multiple inheritance

Interface-driven composition

Modular capability design

Run:

python3 -m ex2.main
🟣 ex3 — Strategy + Factory

Behavior Configuration & Object Creation Abstraction

Strategy Pattern

Encapsulates turn execution logic.

engine.configure_engine(factory, strategy)

Changing strategy ≠ modifying engine.

Abstract Factory Pattern

Encapsulates card creation logic.

The engine depends on CardFactory, not concrete classes.

Separation of Responsibilities

Construction

Behavior

Orchestration

Run:

python3 -m ex3.main
🔴 ex4 — Ranking & Tournament

Interfaces + System Orchestration

Goal

Introduce ranking capability without modifying the core system.

Rankable defines ranking behavior

TournamentCard implements it

TournamentPlatform orchestrates tournament flow

Demonstrates

Interface-driven scalability

ELO-based ranking logic

Orchestration separated from entity logic

Run:

python3 -m ex4.main
🛡 Defense-Ready Explanations
Where is polymorphism?

Every time you see:

card.play(game_state)

The engine never checks the type.
Each subclass defines its own behavior.

Why avoid if card.type == ...?

Because:

Behavior belongs inside the object

Type-checking violates Open/Closed

It centralizes logic and increases coupling

How do you extend the system?

Create a new subclass of Card

Implement play()

Optionally implement additional interfaces

No engine modification required.

That is extensibility by design.

🧪 Linting

From repository root:

flake8

All exercises are flake8 compliant.

🏗 Architectural Summary

DataDeck demonstrates:

Programming to interfaces

Dependency inversion

Controlled multiple inheritance

Pattern application with intent

Open/Closed Principle in practice

Clean, scalable OOP design

🧭 Final Note

This is not a card game.

It is an architecture exercise.

👤 Author

Bea
Python & Backend Developer