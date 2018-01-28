Principles
======

"SOLID"
-------

Follow these principles:

- See <https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)>


The folks at LosTechies.com have created a series of Creative Commons-licenced posters that illustrate the SOLID principles. I took the posters, cleaned up the typography a little and posted them below under the same Creative Commons licence. Below each poster is an explanation of the corresponding SOLID principle. Enjoy!

Single Responsibility Principle
~~~~~~~~~~

.. code-block:: python
    class CarWashService:
        def __init__(self, sms_sender):
            self.sms_sender = sms_sender

        def __call__(self, card_id, customer_id):
            car = Car.objects.get(id=card_id)
            customer = Customer.objects.get(customer_id)
            if car.wash_required:
                car.washed = True
                car.washed_at = utcnow()
                self.sms_sender.send(mobile_phone=customer.phone, text=f"Car %{car.plate} whashed.")



Here is an example model (put this into :file:`models.py`, e.g.)::

    from sqlalchemy import Column, Integer, String
    from yourapplication.database import Base

    class User(Base):
        __tablename__ = 'users'
        id = Column(Integer, primary_key=True)
        name = Column(String(50), unique=True)
        email = Column(String(120), unique=True)

        def __init__(self, name=None, email=None):
            self.name = name
            self.email = email

        def __repr__(self):
            return '<User %r>' % (self.name)

To create the database you can use the `init_db` function:

>>> from yourapplication.database import init_db
>>> init_db()



.. image:: _static/solid/sr.jpg

Open-Closed Principle
~~~~~~~~~~

.. image:: _static/solid/oc.jpg

Liskov Substitution Principle
~~~~~~~~~~

.. image:: _static/solid/ls.jpg

Interface Segregation Principle
~~~~~~~~~~

.. image:: _static/solid/is.jpg

Dependency Inversion Principle
~~~~~~~~~~

.. image:: _static/solid/di.jpg
