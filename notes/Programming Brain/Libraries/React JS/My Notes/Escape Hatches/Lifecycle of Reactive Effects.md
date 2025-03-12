# Lifecycle of Reactive Effects

Effects have a different lifecycle from components. Components may mount, update, or unmount. An Effect can only do two things: to start synchronizing something, and later to stop synchronizing it. This cycle can happen multiple times if your Effect depends on props and state that change over time. React provides a linter rule to check that you’ve specified your Effect’s dependencies correctly. This keeps your Effect synchronized to the latest props and state.

---

![UseEffect_lifecycle.png](Lifecycle%20of%20Reactive%20Effects%201b2aeacbb299814e9cbbfdaef53f66cb/UseEffect_lifecycle.png)

[**The lifecycle of an Effect**](Lifecycle%20of%20Reactive%20Effects%201b2aeacbb299814e9cbbfdaef53f66cb/The%20lifecycle%20of%20an%20Effect%201b2aeacbb29981bcab0de933a1dad50e.md)

[**Effects “react” to reactive values**](Lifecycle%20of%20Reactive%20Effects%201b2aeacbb299814e9cbbfdaef53f66cb/Effects%20%E2%80%9Creact%E2%80%9D%20to%20reactive%20values%201b2aeacbb29981108452eda33e2334b8.md)