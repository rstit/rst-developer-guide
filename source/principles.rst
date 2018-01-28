Principles
======

Single Responsibility Principle
-------

Here is an example of violating this rule::

    class CarWashService:
        def __init__(self, sms_sender):
            self.sms_sender = sms_sender

        def __call__(self, card_id, customer_id):
            car = Car.objects.get(id=card_id)
            customer = Customer.objects.get(customer_id)
            if car.wash_required:
                car.washed = True
                self.sms_sender.send(mobile_phone=customer.phone, text=f"Car %{car.plate} whashed.")

.. image:: _static/solid/sr.jpg

After refactor::

    class CarWashService:
        def __init__(self, repository, notifier):
            self.repository = repository
            self.notifier = notifier

        def __call__(self, car_id, customer_id):
            car = self.repository.get_car(car_id)
            customer = self.repository.get_customer(customer_id)
            if car.wash_required:
                car.washed = True
                self.notifier.wash_completed(customer.phone, car.plate)

Open-Closed Principle
-------

.. image:: _static/solid/oc.jpg

Liskov Substitution Principle
-------

.. image:: _static/solid/ls.jpg

Interface Segregation Principle
-------

.. image:: _static/solid/is.jpg

Dependency Inversion Principle
-------

``Depend of abstractions. Do not depend upon concretion.``


Example with Global State Problem, Implicit Dependency Problem and Concrete API::

class CarWashService:
    def __init__(self, repository):
        self.repository = repository

    def __call__(self, car_id, customer_ids):
        car_wash_job = CarWashJob(car_id, customer_id)
        self.repository.put(car_wash_job)
        SMSNotifier.send_sms(car_wash_job)

.. image:: _static/solid/di.jpg
