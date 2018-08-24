# parreira-manifesto
What I have grook'd

# parreira-manifesto
What I have grook'd

# 1. Systems design

### 1.1 Do NOT factorize for the sake of it
Code duplication is bad. But isolating components just because is equaly bad. Distributed dependencies on code that is more or less immutable over the lifetime of the application/service and does not contain business logic which is critical to system coherency is not required to be factorized or split into components as soon as the need duplication arrives.

Action should be taken if this duplication (or fixes in it) happens a suficient number of times over a short period of time to make it worthwhile to expend effort isolating it. It must be clear to the developer that this will provide a clear advantage over retaining the status quo of _"copy-pasting is fine for this bit"_.

2. Arquitectural decisions

3. W.R.T. creative freedom

4. 

