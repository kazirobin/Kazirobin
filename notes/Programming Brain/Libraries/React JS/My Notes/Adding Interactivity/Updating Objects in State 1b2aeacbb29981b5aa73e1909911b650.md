# Updating Objects in State

State can hold any kind of JavaScript value, including objects. But you shouldn’t change objects that you hold in the React state directly. Instead, when you want to update an object, you need to create a new one (or make a copy of an existing one), and then set the state to use that copy.

---

[What’s a mutation?](Updating%20Objects%20in%20State%201b2aeacbb29981b5aa73e1909911b650/What%E2%80%99s%20a%20mutation%201b2aeacbb299816c9691ee9a6e2832ae.md)

[Treat State As Read-only](Updating%20Objects%20in%20State%201b2aeacbb29981b5aa73e1909911b650/Treat%20State%20As%20Read-only%201b2aeacbb29981bb9112f40321e559f0.md)

[Copying Objects With The Spread Syntax](Updating%20Objects%20in%20State%201b2aeacbb29981b5aa73e1909911b650/Copying%20Objects%20With%20The%20Spread%20Syntax%201b2aeacbb29981bd8868d9cad0370182.md)

[Updating A Nested Object](Updating%20Objects%20in%20State%201b2aeacbb29981b5aa73e1909911b650/Updating%20A%20Nested%20Object%201b2aeacbb29981af97c2d4c83ca1cab7.md)