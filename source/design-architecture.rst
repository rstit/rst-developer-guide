Design Architecture
======


DDD Introduction
------------------

Coupling
~~~~~~~~~~~~~~~~~~
Coupling is the degree of interdependence between software modules.
All project should be loosely coupled. To do this you follow SOLID principles and useone of above clean architecture examples.

Tight Coupling symptoms
~~~~~~~~~~~~~~~~~~
- fat controllers
- fat models
- hard to test
- hard to explain
- hard to read
- spaghetti code

Domain Driven Design Architecture List
~~~~~~~~~~~~~~~~~~
- Clean Architecture
- Haxagonal Architecture (Ports and Adapters)
- Onion Architecture
- Screaming Architecture

Layered Structure
~~~~~~~~~~~~~~~~~~
In DDD approach project should be layered to at least 3 parts.


- Application (glue code)
- Domain (Business Logic)
- Framework (Framework related Interfaces, all can be used as Open Source)


Characteristics
~~~~~~~~~~~~~~~~~~
- Architectures should tell about the system.
- Not about the frameworks.
- New programmers should be able to learn all the use cases of the system.
- And still not know how the system is delivered.
- They may come to you and say: “We see some things that look sorta like models, but where are the views and controllers”, and you should say: “Oh, those are details that needn’t concern you at the moment, we’ll show them to you later.”


DDD Recipes
------------------

Common Project Structure
~~~~~~~~~~~~~~~~~~

Framework layer
~~~~~~~~~~~~~~~~~~
- utils.py
- commons.py
- generics.py
- base.py
- extensions.py
- adapters.py

Domain Layer
~~~~~~~~~~~~~~~~~~
- services.py
- schemas.py
- models.py
- factories.py
- repositories.py
- exceptions.py

Application Layer
~~~~~~~~~~~~~~~~~~
- views.py
- routes.py
- exceptions.py
- app.py
- wsgi.py
- tasks.py
- permissions.py
- authentications.py

Flask/SQLAlchemy Project Structure
~~~~~~~~~~~~~~~~~~
TODO

Django Project Structure
~~~~~~~~~~~~~~~~~~
TODO