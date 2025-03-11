# Separating Events from Effects

Event handlers only re-run when you perform the same interaction again. Unlike event handlers, Effects re-synchronize if some value they read, like a prop or a state variable, is different from what it was during the last render. Sometimes, you also want a mix of both behaviors: an Effect that re-runs in response to some values but not others. This page will teach you how to do that.

---

[**Choosing between event handlers and Effects**](Separating%20Events%20from%20Effects%201b2aeacbb299811cac33ddbf78a032e1/Choosing%20between%20event%20handlers%20and%20Effects%201b2aeacbb2998149997df0b4304ea505.md)

[**Reactive values and reactive logic**](Separating%20Events%20from%20Effects%201b2aeacbb299811cac33ddbf78a032e1/Reactive%20values%20and%20reactive%20logic%201b2aeacbb2998150b422d996a8a6fbd4.md)

[**Extracting non-reactive logic out of Effects**](Separating%20Events%20from%20Effects%201b2aeacbb299811cac33ddbf78a032e1/Extracting%20non-reactive%20logic%20out%20of%20Effects%201b2aeacbb29981908db5cf793a94a3a8.md)