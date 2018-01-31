Documentation
======

Glossary
-----------------
The domain and the technical experts should create document of all the terminology that your team uses in code and issue tracker.
after reading this, there should be no doubt what is happening in the code or what should be done in the task.

Readme
-----------------
A README file at the root directory should give general information to both users and maintainers
of a project. It should be raw text or written in some very easy to read markup, such as
reStructuredText or Markdown. It should contain a few lines explaining the purpose of the project
or library (without assuming the user knows anything about the project), the URL of the main source
for the software. This file should also have information how to configure and run projects for
multiple environments (local, prod, testing). This file is the main entry point for readers of
the code.

example file::

    # Project Title
    One Paragraph of project description goes here

    ## Getting Started
    These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

    ### Prerequisites
    What things you need to install the software and how to install them
    ```
    Give examples
    ```

    ### Installing
    A step by step series of examples that tell you have to get a development env running
    ```
    Give the example
    ```

    ## Running the tests
    Explain how to run the automated tests for this system

    ## Deployment
    Add additional notes about how to deploy this on a live system


API specification
------------------
All backend project should have documented endpoints in apiary.apib file. With this blueprint file
you can already get a mock, documentation and test for your API. This file describe File should be always and up-to-date. Apiary ensures

example file::

    FORMAT: 1A

    # The Simplest API
    This is one of the simplest APIs written in the **API Blueprint**.

    ### List All Questions [GET]
    + Response 200 (application/json)

        + Attributes (array[Question])

    ## Data Structures

    ### Question
    + question: Favourite programming language? (required)
    + published_at: `2014-11-11T08:40:51.620Z` (required)
    + url: /questions/1 (required)
    + choices (array[Choice], required)

    ### Choice
    + choice: Javascript (required)
    + url: /questions/1/choices/1 (required)
    + votes: 2048 (number, required)

Docstring
-----------------
All domain classes should have docstring for class definition. We should create them also
for complex classes and functions that will be used in other places.

.. code-block:: python

    class CarWashService:
        """
        This class describe how to wash a car.
        Service performs advanced and complex actions to wash the customer's car.
        Require repository that could be injected using Dependency Injection.
        After all, calls the function responsible for notifications.
        """
        def __init__(self, repository, notifier):
            self.repository = repository
            self.notifier = notifier

        def __call__(self, car_id, customer_id):
            car = self.repository.get_car(car_id)
            customer = self.repository.get_customer(customer_id)
            if car.wash_required:
                car.washed = True
                car.washed_at = utcnow()
                self.notifier.wash_completed(customer.phone, car.plate)
            return car

Type Hint
-----------------
If there is such a possibility, we should use it wherever possible. This will allow showing
explicitly what we expect and what will be returned.

.. code-block:: python

class CarWashService:
    """
    This class describe how to wash a car.
    Service performs advanced and complex actions to wash the customer's car.
    Require repository that could be injected using Dependency Injection.
    """
    def __init__(self, repository: MongoRepository, notifier: SMSNotifier) -> None:
        self.repository = repository
        self.notifier = notifier

    def __call__(self, car_id: int, customer_id: int) -> Car:
        """
        :param car_id:              Unique Identifier of a Car
        :param customer_id:         Unique Identigier of a Customer
        :return:
        """
        car = self.repository.get_car(car_id)
        customer = self.repository.get_customer(customer_id)
        if car.wash_required:
            car.washed = True
            car.washed_at = utcnow()
            self.notifier.wash_completed(customer.phone, car.plate)
        return car
