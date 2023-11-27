# What is the Single-Responsibility Principle (SRP)?

- The Single-responsibility Principle, or SRP, states that a class should only have one reason to change. This means that a class should have only one job and do one thing.
    - So lets say you have a class or (object) and lets name it ValidatePerson , you will want this one class (class can also mean object just to clear up any confusion) to do a singular thing, however that singular thing can be something like (ValidateName() and ValidateAge()), it would be considered a single responsibility because they both are direct children within "how" the Person is Validated. So lets say you have a person walk into a bar, that person hands you an ID, you want to "ValidatePerson" by checking their name (ValidateName()) and their age (ValidateAge()), however you may want to check their picture, which would bring us to our issue where you'll always be tempted to put similar classes together - but unfortunately, this goes against the Single-responsibility principle. Why? Let's take a look at a proper example to explain the issue if we were to put in a Display() method.

    - The ValidatePerson object below has three methods:
        - Two validation methods, (ValidateName() and ValidateAge()), and a Display() method.

```JS
class ValidatePerson{
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    ValidateName(name) {
        if (name.length > 3){
            return true;
        } else{
            return false;
        }
    }

    ValidateAge(age) {
        if (age > 21){
            return true;
        } else{
            return false;
        }
    }

    Display() {
        if (this.ValidateName(this.name) && this.ValidateAge(this.age)) {
            console.log(`Name: ${this.name} and Age: ${this.age}`);
        } else {
            console.log('Invalid');
        }
    }
}
```

- The Display() method goes against the SRP because the goal is that a class should have only one job and do one thing.
    - The ValidatePerson class does two jobs - it validates the person's name and age, and then displays some information.
    - To avoid confusion, yes, the ValidateName() and ValidateAge() job(s) are considered "one" job.

- The way to avoid this problem is to separate code that supports different actions and jobs so that each class only performs one job and has one reason to change.

- This means that the ValidatePerson class will only be responsible for validating a person (user), as seen below:

```JS
class ValidatePerson {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    ValidateName(name) {
        if (name.length > 3) {
            return true;
        } else {
            return false;
        }
    }

    ValidateAge(age) {
        if (age > 21) {
            return true;
        } else {
            return false;
        }
    }
}
```
- While the new class DisplayPerson will now be responsible for displaying a person, as you can see in the code block below:

```JS
class DisplayPerson {
    constructor(name, age) {
        this.name = name;
        this.age = age;
        this.validate = new ValidatePerson(this.name, this,age);
    }

    Display() {
        if (
            this.validate.ValidateName(this.name) &&
            this.validate.ValidateAge(this.age)
        ) {
            console.log(`Name: ${this.name} and Age: ${this.age}`);
        } else {
            console.log('Invalid');
        }
    }
}
```