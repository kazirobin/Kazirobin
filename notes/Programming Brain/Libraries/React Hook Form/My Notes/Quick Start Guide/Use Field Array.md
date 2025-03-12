# Use Field Array

First, let’s start by installing the necessary dependencies. You will need to install the React Hook Form library and the useFieldArray hook. You can do this by running the following command in your terminal:

```jsx
npm install react-hook-form
```

Once you have installed the dependencies, you can start implementing the useFieldArray hook in your React form. Here’s an example of how to use the hook:

```jsx
import { useForm, useFieldArray } from 'react-hook-form';
function MyForm() {
 const { register, control, handleSubmit } = useForm({
 defaultValues: {
 items: [{ name: 'item1' }, { name: 'item2' }],
 },
 });
 const { fields, append, remove } = useFieldArray({
 control,
 name: 'items',
 });
const onSubmit = (data) => console.log(data);
return (
 <form onSubmit={handleSubmit(onSubmit)}>
 {fields.map((field, index) => (
 <div key={field.id}>
 <input
 {…register(`items.${index}.name`)}
 defaultValue={field.name}
 />
 <button type="button" onClick={() => remove(index)}>
 Remove
 </button>
 </div>
 ))}
 <button type="button" onClick={() => append({ name: '' })}>
 Add Item
 </button>
 <button type="submit">Submit</button>
 </form>
 );
}
export default MyForm;
```

In this example, we are using the useForm hook to initialize our form with default values. We are also using the useFieldArray hook to manage the “items” field array. The “control” prop is passed to the useFieldArray hook to allow it to interact with the useForm hook.

The fields.map function is used to render each input field in the “items” array. The remove function is called when the “Remove” button is clicked, and the append function is called when the “Add Item” button is clicked.

By using the useFieldArray hook, we can easily add or remove fields in our form without having to manually manage the state of the form. This makes it easier to create complex forms with dynamic inputs.

But what if we want to use more than one field in the “items” array? No problem! You can simply add more inputs to the form. Here’s an example that includes two fields (“name” and “quantity”) in the “items” array:

```jsx
import { useForm, useFieldArray } from 'react-hook-form';
function MyForm() {
 const { register, control, handleSubmit } = useForm({
 defaultValues: {
 items: [{ name: 'item1', quantity: 1 }, { name: 'item2', quantity: 2 }],
 },
 });
 const { fields, append, remove } = useFieldArray({
 control,
 name: 'items',
 });
const onSubmit = (data) => console.log(data);
return (
 <form onSubmit={handleSubmit(onSubmit)}>
 {fields.map((field, index) => (
 <div key={field.id}>
 <input
 {…register(`items.${index}.name`)}
 defaultValue={field.name}
 />
 <input
 {…register(`items.${index}.quantity`)}
 defaultValue={field.quantity}
 />
 <button type="button" onClick={() => remove(index)}>
 Remove
 </button>
 </div>
 ))}
 <button type="button" onClick={() => append({ name: '', quantity: 0 })}>
 Add Item
 </button>
 <button type="submit">Submit</button>
 </form>
 );
}
export default MyForm;
```

In this updated example, we have added a second input field for “quantity”. We are using the same approach as before to render each input field in the “items” array. The remove function is still called when the “Remove” button is clicked, and the append function is still called when the “Add Item” button is clicked.

By using the useForm and useFieldArray hooks together, we can easily manage complex forms with multiple inputs in React JS. The useFieldArray hook is a powerful tool that allows us to dynamically add or remove fields in a form, making it easier to create dynamic and user-friendly forms.