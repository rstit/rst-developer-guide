Principles
======

In short, where this principles actually pay off:

- Readability — Having simple objects defined based on what they do make our life a lot easier coming back to the code we wrote months ago.
- Testability — Since the signatures of the objects are well-defined and very much contained, creating unit and integration tests is super straightforward and fast.
- Robustness — Simple objects allow you to focus on the specificities of each task individually and reduces the amount of input/output variables you need to consider at any given time. Thus making the whole process less error-prone.
- Onboarding — This approach has proven itself very helpful when handing down knowledge as the thought process is like a standard line protocol instead of a wibbly wobbly mix of instructions.
- Caching Layers — For scaling scenarios, you can cache objects using solutions such as Redis just by adding 2/3 lines of code to an object. As such you don't need interfere with the rest of the codebase.
- Reusability — Given all the examples we've seen, I think this speaks for itself.
- Less Issues — Considerably reduces cyclomatic complexity, hence, reducing the amount of defects


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

example::

    class Rectangle(object):

        def __init__(self, width, height):
            self.width = width
            self.height = height

    class AreaCalculator(object):

        def __init__(self, shapes):

            assert isinstance(shapes, list), "`shapes` should be of type `list`."
            self.shapes = shapes

        @property
        def total_area(self):
            total = 0
            for shape in self.shapes:
                total += shape.width * shape.height

            return total

    def main():
        shapes = [Rectangle(2, 3), Rectangle(1, 6)]
        calculator = AreaCalculator(shapes)
        print(calculator.total_area)

.. image:: _static/solid/oc.jpg

after refactor You can see that it will be easy to extend the functionality::

    from abc import ABCMeta, abstractproperty

    class Shape(object):
        __metaclass__ = ABCMeta

        @abstractproperty
        def area(self):
            pass

    class Rectangle(Shape):

        def __init__(self, width, height):
            self.width = width
            self.height = height

        @property
        def area(self):
            return self.width * self.height

    class AreaCalculator(object):

        def __init__(self, shapes):
            self.shapes = shapes

        @property
        def total_area(self):
            total = 0
            for shape in self.shapes:
                total += shape.area
            return total

    def main():
        shapes = [Rectangle(1, 6), Rectangle(2, 3)]
        calculator = AreaCalculator(shapes)

        print(calculator.total_area)

Liskov Substitution Principle
-------

This is a scary term for a very simple concept. It's formally defined as "If S is a subtype of T, then objects of type T may be replaced with objects of type S (i.e., objects of type S may substitute objects of type T) without altering any of the desirable properties of that program (correctness, task performed, etc.)." That's an even scarier definition.

The best explanation for this is if you have a parent class and a child class, then the base class and child class can be used interchangeably without getting incorrect results. This might still be confusing, so let's take a look at the classic Square-Rectangle example. Mathematically, a square is a rectangle, but if you model it using the "is-a" relationship via inheritance, you quickly get into trouble.

Example::

    class Rectange:

        def __init__(self):
            self.width = 0
            self.height = 0

        def set_width(self, width):
            self.width = width

        def set_height(self, height):
            self.height = height

        def set_color(self, color):
            self.color = color

        def render(self):
            # ...

    class Squere(Rectange):

        def set_width(self, width):
            self.width = width
            self.height = width

        def set_height(self, height):
            self.height = height
            self.width = height

.. image:: _static/solid/ls.jpg

After refactor::

    class Shape:
        def set_color(self, color):
            self.color = color

        def render(self):
        # ...

    class Rectange(Shape):
        def __init__(self, width, heigh):
            self.width = width
            self.height = heigh

        def get_area(self):
            return self.width * self.height

    class Square(Shape):
        def __init__(self, length):
            self.length

        def get_area(self):
            return self.length * self.length


Interface Segregation Principle
-------

.. code-block::python

    class APIView:
        def get(self, id):
            qs = self.get_query_string()
            data = self.get_order_data(id, qs.get('color'))
            return json.dump(), 200

        def get_query_string(self):
            return self.request.qs.parse()

        def get_order_data(self, id, color):
            return Order.objects.filter(id=id, color=color)

.. image:: _static/solid/is.jpg

 after refactor::

    class APIView:
        repo = OrderRepo()

        def get(self, id):
            qs = self.get_query_string()
            data = self.repo.get_order_data(id, qs.get('color'))
            return json.dump(), 200

        def get_query_string(self):
            return self.request.qs.parse()

    class OrderRepo:

        def get_order_data(self, id, color):
            return Order.objects.filter(id=id, color=color)


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


After refactor::

    class CarWashService:
        def __init__(self, notifier, repository):
            self.repository = repository
            self.notifier = notifier

        def __call__(self, car_id, customer_id):
            car_wash_job = CarWashJob(car_id, customer_id)
            self.repository.put(car_wash_job)
            self.notifier.job_completed(car_wash_job)

