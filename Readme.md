# Take-home challenge

Hey there!

As part of the interview process, we ask candidates to do a short take-home challenge. This helps us to understand the programming skills of potential team members.

If you’d like to participate, here is the exercise.

## Exercise: small front + backend app
We are going to create an app to calculate how many people could travel on a list of vehicles.

Given this table:

| ID  | Type of vehicle | Max number of passengers  |
|-----|:---------------:|:-------------------------:|
| M   |    Motorbike    |             1             |
| C   |       Car       |             5             |
| B   |       Bus       |            30             |
| T   |      Train      |            200            |


## Frontend:

Use Angular to create a frontend. Display a page with 2 sections:

**Section 1: a label + input + submit button and a potential result.**

On the left side of the page, there is going to be a small form with a ‘Insert a list of vehicles’ label, then an input where a user can insert a string with an unordered list of vehicle IDs (for example: ‘BMCMBT’), and then a ‘Submit’ button.

If the user submits a value, the front is going to send a POST request to the backend, and then display a result below the form: “Ideal number of passengers: <result>”.

**Section 2: a list of previous results.**

On the right side of the page, there is going to be a title “Previous results”, and then a list displaying elements in the form of “[Input N]: [Result N]” (for example: “MCM: 7”).

Please note, previous values will be displayed even after refreshing the page (they will be ‘persisted’ in the backend).

**Responsive design:**

When the navigator width is below 800px, display one section below the other.

## Backend:

Use Spring Boot to create a backend. It should have at least three different packages: controllers, domain, and database.

### Controllers package

This package should have a single controller with 2 endpoints available:


**POST /passengers**

Expects a body with this JSON format { input: “<inputString>” }
When a request is received, the system should:
Take the inputString and do the following steps with each char / ID:
Parse the ID and create an object of the adequate domain class.
Use a method called .getIdealNumberOfPassengers() to get a value to be summed with the rest.
Once everything has been summed, “persist” the original input and the result in the FakeDB.
Then return a JSON to the frontend with the following format: { input: “<inputString>”, idealNumberOfPassengers: <output number>}.

**GET /passengers**

This endpoint is gonna return a JSON array with the previous inputs and result (same JSON format than the previous request). The values should be taken from the FakeDB.
No need to implement pagination here.

For this exercise, it’s okay to include some application logic in the controller.

### Domain package
You should use this package to design a class hierarchy to support the potential vehicles. Remember that there should be a method called .getIdealNumberOfPassengers() to get the value associated with each type of vehicle. Tip: use polymorphism!

### Database package

IMPORTANT: WE ARE NOT GOING TO USE A REAL DATABASE.

For simplicity, let’s create a simple implementation of an in-memory database that satisfies these conditions:


There is going to be only one class in the package called FakeDB.
FakeDB should implement the singleton pattern, and should be used from other packages as singletons are supposed to be used.
At an object level, FakeDB instances should have these public methods:
insertNewCalculation(input, idealPassengers); // You could return a value if you think it’s valuable.
getPreviousCalculations(); //This return a list / collection of values.
You’re free to use all the private fields or methods that you want.

Again, this is supposed to be a mock. There is no need to use any external technology, we just need the simplest solution that does the job (just remember to use the singleton pattern). The results are expected to disappear when the Spring Boot Application is stopped.

### What are we going to evaluate.

- Code readability: no need to minimize the number of lines in the code, if an extra line or function means that the code is easier to read, please do it.
- Framework knowledge: nothing complex is required, just the ability to use the framework's tools for the job.
- Object-oriented programming (OOP): the ability to design or implement a structure of classes that uses polymorphism to achieve the job.
- Design patterns: detecting opportunities to apply programming design patterns.
- Support material: if you think it’s valuable to mention something about some choices or criteria used in the code, feel free to include a Readme.md / txt / doc to provide your thoughts.

### What are we NOT going to evaluate (so no need to do it).

- UI styles: no need to invest time in styling the page in a fancy web. Only do what was required: responsive updates and maybe alignments.
- Angular components: no need to create multiple angular comments. You can do everything in a single component.
- No need for any configuration file: feel free to hardcode values if needed (tip: create a constant if a value is expected to be used in multiple places).
- Form validation in the frontend is not needed.
- Unit tests are not needed.
