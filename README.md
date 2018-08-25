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
