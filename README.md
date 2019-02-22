# The Parreira Manifesto
What I have grook'd

# 1. W.R.T. systems design

### 1.1 Do NOT factorize for the sake of it
Code duplication is bad. But isolating components for the sake of it can be -in some regard, worse- equaly as bad. Distributed dependencies on code that is more or less immutable over the lifetime of the application/service and does not contain business logic which is critical to system coherency is not required to be factorized or split into components as soon as the need duplication arrives.

Action should be taken when the duplicated excerpt this duplication (or fixes in it) happens a suficient number of times over a short period of time to make it worthwhile to expend effort isolating it. It must be clear to the developer that this will provide a clear advantage over retaining the status quo of *"copy-pasting is fine for this bit"*.

# 2. W.R.T. arquitectural decisions

### 3.1 Trends can be considered, but should NEVER accepted unilateraly 

> TODO microservices for the hell of it
> TODO dependency injection because its what was being done forever
> TODO trying to force new technologies that put team out of depth without a good enough reason to experiment
> TODO 

# 3. W.R.T. creative freedom

### 3.1 Attrittion to change is self-planned obsolescence
The opportunity to dabble in change represents growth. Even when this potential growth transforms itself into an experience which we would not like to repeat, these points of reference will be useful in the future when emerging ourselves into new paradigms. Obviously, positive experiences are prefered since they will provide useful points of reference that could be directly applied in future efforts. Conversely, sometimes negative experiences can lead to a much more prominent growth spurt in onself and a warning sign of what to avoid in the future. But situations change, and technology changes, so even negative experiences should be periodically *given a chance*  to access it's validity.

### 3.2 Code as craft, NOT an extension of ego
Some say programming is a type of art. It is not binary, there are no absolute right or wrongs. It can be a vehicle for the expression of an individual for whom their product is transitively, a part of themselves. 
This brings attachment to the code which can lead to the original writter to adopt a certain protectionism towards it which will be damaging. The creator will avoid exploring alternatives that would imply a defect in the original creation. His collaborators, on the other hand, will try avoid clashing with the creator and destroying his creation which is negative for both sides.

It boils down to the personality of the developer, and more common across the ones that are really passionate about their craft. But in the end, it is a negative trait with negative consequences that one should strive to remove from his repertoire.

# 4. W.R.T performance

> TODO are we designing for a system which will handle the load in 1-2 years 
> TODO is expected performance of platform important enough to pre-optimize for it

# 5. W.R.T testing

### 5.1 Avoid reuse of unit test object
Do not hardcode unit tests (static) objects in the class and reuse them everywhere. It might look cleaner and nicer but it will bring maintainability issues down the line. If something is to be refactored and the connections between these are hardcoded (foreign key ids) it will be very hard to refactor away. Better to create new objects in the method's test itself (even if it's copy pasted). Tests shouldn't have dependencies to one another.


    private val episodeOrder1 = Order(
            UUID.randomUUID().toString(),
            1,
            "Magic",
            "type",
            campaignId1,
            25,
            UUID.randomUUID().toString(),
            DateTime.now(),
            "status",
            null,
            null,
            null
    )

    private val OrderTask1 = OrderTask(
            Order1.id,
            "type",
            DateTime.now(),
            DateTime.now(),
            DateTime.now(),
            DateTime.now(),
            "status"
    )

    // if I have to refactor the id away for example, there will be a lot of code to change because I won't know the id of it until it executes at runtime


### 5.2 Avoid chaos - avoid randomness
If you are creating unit tests, AVOID using UUID.randomUUID()! Unit tests should be as reproducible as possible for obvious reasons. In this case, if we really don't care about the value of that UUID in particular, the best choice is to generate a UUID ahead of time (https://www.uuidgenerator.net/version4 or REPL)

### 5.3 Makes sure tests use different database instances
If test are using a database and are independent (they should), please reinstantiate/clean the DB between tests. Many of the issues that might happen due to unexpected state of the database between test executions can be attributed to a shared database instance, most of the time attributes to the lazyness of having to re-instantiate it. It is, however, always worth the extra effort to do so.

    protected val db = Database.connect(
            "jdbc:h2:mem:test${UUID.randomUUID()};DB_CLOSE_DELAY=-1;MODE=MYSQL;",
            "org.h2.Driver",
            "root",
            "mirriad"
    )

### 5.4 Do not compare complex objects based on their x.toString()
If you change object implementation or replace one of the classes being used in the DB/responses (as it should) this will start failing due to different field/class names. Better to just do a lot of copy-paste and enumerate all the fields and compare them manually (learn multi-line editing in your favourite editor).

        val expected = Order(
                1,
                "Wonderful adventures of nobody",
                "some type",
                10,
                DateTime.now(),
                "some status",
                null,
                null,
                null
        )

        ...

        assertEquals(expected.toString(), repository.findById(id).toString())

# 6. W.R.T kotlin specific advice

### 6.1 Use dictionary-addressing when having 2/3+ parameters
In Kotlin, one of the most powerful features is the dictionary-addressing for parameters when calling functions (f(a=1,b=2,..)). This is just delegating the burden to the compiler because it does the exact same at runtime - put stuff in the correct order in the stack for the calling function to use. When methods have a lot of parameters (eg: data classes), it is worth to use this addressing. That way, if something is changed in future regarding this function like parameter order or adition/removal of parameters, we won't have to change the whole thing. Besides being a lot more visible and avoiding human error because the parameter being binded is a lot more obvious to the developer reading the code.

    private val Order1 = Order(
            // UUID.randomUUID().toString(),
            1,
            "Magic",
            "type",
            campaignId1,
            25,
            UUID.randomUUID().toString(),
            DateTime.now(),
            "status",
            null,
            null,
            null
    )

    // I removed/moved the "id" field, and now I to go to all places where this class is created and modify it as well. In some cases, this won't even be a compile-time error if all other fields types happen to match afterwards and the number of parameters might not raise an error if the last parameters had default values on them!






# TODO - left to develop/categorize
- Always mistrust round or close to round numbers. If a query is now showing everything that you expect and has exactly or close to 500 elements (as example), i might be getting capped or limited somewhere.
