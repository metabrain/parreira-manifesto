# The Parreira Manifesto
What I have grook'd

# 1. W.R.T. systems design

### 1.1 Do NOT factorize for the sake of it
Code duplication is bad. But isolating components for the sake of it can be -in some regard, worse- equaly as bad. Distributed dependencies on code that is more or less immutable over the lifetime of the application/service and does not contain business logic which is critical to system coherency is not required to be factorized or split into components as soon as the need duplication arrives.

Action should be taken when the duplicated excerpt this duplication (or fixes in it) happens a suficient number of times over a short period of time to make it worthwhile to expend effort isolating it. It must be clear to the developer that this will provide a clear advantage over retaining the status quo of _"copy-pasting is fine for this bit"_.

# 2. W.R.T. arquitectural decisions

# 3. W.R.T. creative freedom

### 3.1 Attrittion to change is self-planned obsolescence
The opportunity to dabble in change represents growth. Even when this potential growth transforms itself into an experience which we would not like to repeat, these points of reference will be useful in the future when emerging ourselves into new paradigms. Obviously, positive experiences are prefered -debatable, since I believe that sometimes negative experiences can lead to more acute growth in onself- for 

# 4. W.R.T performance
