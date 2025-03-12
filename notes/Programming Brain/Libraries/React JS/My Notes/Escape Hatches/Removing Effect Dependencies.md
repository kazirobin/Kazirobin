# Removing Effect Dependencies

When you write an Effect, the linter will verify that you’ve included every reactive value (like props and state) that the Effect reads in the list of your Effect’s dependencies. This ensures that your Effect remains synchronized with the latest props and state of your component. Unnecessary dependencies may cause your Effect to run too often, or even create an infinite loop. Follow this guide to review and remove unnecessary dependencies from your Effects.

---

[**Dependencies should match the code**](Removing%20Effect%20Dependencies%201b2aeacbb299815d9d92e59f45f61dbd/Dependencies%20should%20match%20the%20code%201b2aeacbb29981249a06ded6491f146d.md)

[**Removing unnecessary dependencies**](Removing%20Effect%20Dependencies%201b2aeacbb299815d9d92e59f45f61dbd/Removing%20unnecessary%20dependencies%201b2aeacbb29981a4aa14cd903d5b15af.md)