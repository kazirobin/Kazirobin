# Choosing The State Structure

`CreatedAt- 24 Jan 2024 / RevisedAt-`

Structuring state well can make a difference between a component that is pleasant to modify and debug, and one that is a constant source of bugs. Here are some tips you should consider when structuring state.

## Principles for structuring state

When you write a component that holds some state, you’ll have to make choices about how many state variables to use and what the shape of their data should be. While it’s possible to write correct programs even with a suboptimal state structure, there are a few principles that can guide you to make better choices:

1. **Group related state.** If you always update two or more state variables at the same time, consider merging them into a single state variable.
2. **Avoid contradictions in state.** When the state is structured in a way that several pieces of state may contradict and “disagree” with each other, you leave room for mistakes. Try to avoid this.
3. **Avoid redundant state.** If you can calculate some information from the component’s props or its existing state variables during rendering, you should not put that information into that component’s state.
4. **Avoid duplication in state.** When the same data is duplicated between multiple state variables, or within nested objects, it is difficult to keep them in sync. Reduce duplication when you can.
5. **Avoid deeply nested state.** Deeply hierarchical state is not very convenient to update. When possible, prefer to structure state in a flat way.

The goal behind these principles is to *make state easy to update without introducing mistakes*. Removing redundant and duplicate data from state helps ensure that all its pieces stay in sync. This is similar to how a database engineer might want to [“normalize” the database structure](https://docs.microsoft.com/en-us/office/troubleshoot/access/database-normalization-description) to reduce the chance of bugs. To paraphrase Albert Einstein, **“Make your state as simple as it can be—but no simpler.”**

Now let’s see how these principles apply in action.

[**Group related state**](Choosing%20The%20State%20Structure%201b2aeacbb29981948a1cd6901ec68d41/Group%20related%20state%201b2aeacbb29981d786d8ff8516e2f30c.md)

[**Avoid contradictions in state**](Choosing%20The%20State%20Structure%201b2aeacbb29981948a1cd6901ec68d41/Avoid%20contradictions%20in%20state%201b2aeacbb29981dc85fcde96efe77113.md)

[**Avoid redundant state**](Choosing%20The%20State%20Structure%201b2aeacbb29981948a1cd6901ec68d41/Avoid%20redundant%20state%201b2aeacbb29981adbe22e8527c750568.md)

[**Avoid duplication in state**](Choosing%20The%20State%20Structure%201b2aeacbb29981948a1cd6901ec68d41/Avoid%20duplication%20in%20state%201b2aeacbb29981499791d11677b15459.md)

[**Avoid deeply nested state**](Choosing%20The%20State%20Structure%201b2aeacbb29981948a1cd6901ec68d41/Avoid%20deeply%20nested%20state%201b2aeacbb2998136b432c47aed92f947.md)