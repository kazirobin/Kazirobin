# Props Validation

Props are an important mechanism for passing the read-only attributes to React components. The props are usually required to use correctly in the component. If it is not used correctly, the components may not behave as expected. Hence, it is required to use props validation in improving react components.

ReactJS props validator contains the following list of validators.

| **PropTypes** | **Description** |
| --- | --- |
| PropTypes.any | The props can be of any data type. |
| PropTypes.array | The props should be an array. |
| PropTypes.bool | The props should be a boolean. |
| PropTypes.func | The props should be a function. |
| PropTypes.number | The props should be a number. |
| PropTypes.object | The props should be an object. |
| PropTypes.string | The props should be a string. |
| PropTypes.symbol | The props should be a symbol. |
| PropTypes.instanceOf | The props should be an instance of a particular JavaScript class. |
| PropTypes.isRequired | The props must be provided. |
| PropTypes.element | The props must be an element. |
| PropTypes.node | The props can render anything: numbers, strings, elements or an array (or fragment) containing these types. |
| PropTypes.oneOf() | The props should be one of several types of specific values. |
| PropTypes.oneOfType([PropTypes.string,PropTypes.number]) | The props should be an object that could be one of many types. |

## Example

```jsx
App.propTypes = {  
    propArray: PropTypes.array.isRequired,  
    propBool: PropTypes.bool.isRequired,  
    propFunc: PropTypes.func,  
    propNumber: PropTypes.number,  
    propString: PropTypes.string,   
}
```

```jsx
App.defaultProps = {  
    propArray: [1,2,3,4,5],  
    propBool: true,  
    propFunc: function(x){return x+5},  
    propNumber: 1,  
    propString: "JavaTpoint",  
}
```