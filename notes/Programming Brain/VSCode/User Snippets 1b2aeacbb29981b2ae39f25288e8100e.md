# User Snippets

Code snippets are templates that make it easier to enter repeating code patterns, such as loops or conditional statements. In Visual Studio Code, snippets appear in IntelliSense (Ctrl+Space) mixed with other suggestions, as well as in a dedicated snippet picker (Insert Snippet in the Command Palette).

---

- React VS Code Snippets For TypeScript JSX
    
    ```json
    {
    	// Import React
    	"importReact": {
    		"key": "importReact",
    		"prefix": "imr",
    		"body": [
    			"import React from 'react'"
    		]
    	},
    	//React Arrow Function Component With Name Export
    	"reactArrowFunctionComponent": {
    		"key": "reactArrowFunctionComponent",
    		"prefix": "rafc",
    		"body": [
    			"export const ${1} = () => {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			""
    		],
    		"description": "Creates a React Arrow Function Component with ES7 module system"
    	},
    	//React Arrow Function Component With Export Default
    	"reactArrowFunctionExportComponent": {
    		"key": "reactArrowFunctionExportComponent",
    		"prefix": "rafce",
    		"body": [
    			"const ${1} = () => {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			"",
    			"export default ${1}"
    		],
    		"description": "Creates a React Arrow Function Component with ES7 module system"
    	},
    	//React Function Component With Export Default
    	"reactFunctionalComponent": {
    		"key": "reactFunctionalComponent",
    		"prefix": "rfc",
    		"body": [
    			"export default function ${1}() {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			""
    		],
    		"description": "Creates a React Functional Component with ES7 module system"
    	},
    	// React Function Component With Separate Export Default
    	"reactFunctionalExportComponent": {
    		"key": "reactFunctionalExportComponent",
    		"prefix": "rfce",
    		"body": [
    			"function ${1}() {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			"",
    			"export default ${1}"
    		],
    		"description": "Creates a React Functional Component with ES7 module system"
    	},
    	// Console Log
    	"consoleLog": {
    		"key": "consoleLog",
    		"prefix": "clg",
    		"body": [
    			"console.log(${1})"
    		],
    		"description": "Displays a message in the console"
    	},
    	// Console Dir
    	"consoleDir": {
    		"key": "consoleDir",
    		"prefix": "cdi",
    		"body": [
    			"console.dir(${1})"
    		],
    		"description": "Prints a JavaScript representation of the specified object"
    	},
    	// Console clear
    	"consoleClear": {
    		"key": "consoleClear",
    		"prefix": "ccl",
    		"body": [
    			"console.clear()"
    		],
    		"description": "Clears the console",
    	},
    	// Console error
    	"consoleError": {
    		"key": "consoleError",
    		"prefix": "cer",
    		"body": [
    			"console.error(${1})"
    		],
    		"description": "Displays a message in the console and also includes a stack trace from where the method was called",
    	}
    }
    ```
    
- React VS Code Snippets For JavaScript JSX
    
    ```json
    {
    	// Import React
    	"importReact": {
    		"key": "importReact",
    		"prefix": "imr",
    		"body": [
    			"import React from 'react'"
    		]
    	},
    	//React Arrow Function Component With Name Export
    	"reactArrowFunctionComponent": {
    		"key": "reactArrowFunctionComponent",
    		"prefix": "rafc",
    		"body": [
    			"export const ${1} = () => {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			""
    		],
    		"description": "Creates a React Arrow Function Component with ES7 module system"
    	},
    	//React Arrow Function Component With Export Default
    	"reactArrowFunctionExportComponent": {
    		"key": "reactArrowFunctionExportComponent",
    		"prefix": "rafce",
    		"body": [
    			"const ${1} = () => {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			"",
    			"export default ${1}"
    		],
    		"description": "Creates a React Arrow Function Component with ES7 module system"
    	},
    	//React Arrow Function Component With Export Default And Prop Types
    	"reactArrowFunctionComponentWithPropTypes": {
    		"key": "reactArrowFunctionComponentWithPropTypes",
    		"prefix": "rafcp",
    		"body": [
    			"import PropTypes from 'prop-types'",
    			"",
    			"const ${1} = props => {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			"",
    			"${1}.propTypes = {}",
    			"",
    			"export default ${1}"
    		],
    		"description": "Creates a React Arrow Function Component with ES7 module system with PropTypes"
    	},
    	//React Function Component With Export Default
    	"reactFunctionalComponent": {
    		"key": "reactFunctionalComponent",
    		"prefix": "rfc",
    		"body": [
    			"export default function ${1}() {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			""
    		],
    		"description": "Creates a React Functional Component with ES7 module system"
    	},
    	//React Function Component With Export Default And Prop Types
    	"reactFunctionalComponentWithPropTypes": {
    		"key": "reactFunctionalComponentWithPropTypes",
    		"prefix": "rfcp",
    		"body": [
    			"import PropTypes from 'prop-types'",
    			"",
    			"export default function ${1}(props) {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			"",
    			"${1}.propTypes = {}",
    			""
    		],
    		"description": "Creates a React Functional Component with ES7 module system with PropTypes"
    	},
    	// React Function Component With Separate Export Default
    	"reactFunctionalExportComponent": {
    		"key": "reactFunctionalExportComponent",
    		"prefix": "rfce",
    		"body": [
    			"function ${1}() {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			"",
    			"export default ${1}"
    		],
    		"description": "Creates a React Functional Component with ES7 module system"
    	},
    	// Console Log
    	"consoleLog": {
    		"key": "consoleLog",
    		"prefix": "clg",
    		"body": [
    			"console.log(${1})"
    		],
    		"description": "Displays a message in the console"
    	},
    	// Console Dir
    	"consoleDir": {
    		"key": "consoleDir",
    		"prefix": "cdi",
    		"body": [
    			"console.dir(${1})"
    		],
    		"description": "Prints a JavaScript representation of the specified object"
    	},
    	// Console clear
    	"consoleClear": {
    		"key": "consoleClear",
    		"prefix": "ccl",
    		"body": [
    			"console.clear()"
    		],
    		"description": "Clears the console",
    	},
    	// Console error
    	"consoleError": {
    		"key": "consoleError",
    		"prefix": "cer",
    		"body": [
    			"console.error(${1})"
    		],
    		"description": "Displays a message in the console and also includes a stack trace from where the method was called",
    	}
    }
    ```
    
- React VS Code Snippets For JavaScript
    
    ```json
    {
    	// Console Log
    	"consoleLog": {
    		"key": "consoleLog",
    		"prefix": "clg",
    		"body": [
    			"console.log(${1})"
    		],
    		"description": "Displays a message in the console"
    	},
    	// Console Dir
    	"consoleDir": {
    		"key": "consoleDir",
    		"prefix": "cdi",
    		"body": [
    			"console.dir(${1})"
    		],
    		"description": "Prints a JavaScript representation of the specified object"
    	},
    	// Console clear
    	"consoleClear": {
    		"key": "consoleClear",
    		"prefix": "ccl",
    		"body": [
    			"console.clear()"
    		],
    		"description": "Clears the console",
    	},
    	// Console error
    	"consoleError": {
    		"key": "consoleError",
    		"prefix": "cer",
    		"body": [
    			"console.error(${1})"
    		],
    		"description": "Displays a message in the console and also includes a stack trace from where the method was called",
    	},
    	//JavaScript Arrow Function
    	"javascriptArrowFunction": {
    		"key": "javascriptArrowFunction",
    		"prefix": "jaf",
    		"body": [
    			"const ${1} = () => {",
    			"   ${2}",
    			"}",
    		],
    		"description": "Creates a JavaScript Arrow Function with ES7 module system"
    	},
    	//JavaScript Regular Function
    	"javascriptRegularFunction": {
    		"key": "javascriptRegularFunction",
    		"prefix": "jrf",
    		"body": [
    			"function ${1}() {",
    			"   ${2}",
    			"}",
    		],
    		"description": "Creates a JavaScript Regular Function with ES7 module system"
    	},
    	// Import React
    	"importReact": {
    		"key": "importReact",
    		"prefix": "imr",
    		"body": [
    			"import React from 'react'"
    		]
    	},
    	//React Arrow Function Component With Name Export
    	"reactArrowFunctionComponent": {
    		"key": "reactArrowFunctionComponent",
    		"prefix": "rafc",
    		"body": [
    			"export const ${1} = () => {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			""
    		],
    		"description": "Creates a React Arrow Function Component with ES7 module system"
    	},
    	//React Arrow Function Component With Export Default
    	"reactArrowFunctionExportComponent": {
    		"key": "reactArrowFunctionExportComponent",
    		"prefix": "rafce",
    		"body": [
    			"const ${1} = () => {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			"",
    			"export default ${1}"
    		],
    		"description": "Creates a React Arrow Function Component with ES7 module system"
    	},
    	//React Arrow Function Component With Export Default And Prop Types
    	"reactArrowFunctionComponentWithPropTypes": {
    		"key": "reactArrowFunctionComponentWithPropTypes",
    		"prefix": "rafcp",
    		"body": [
    			"import PropTypes from 'prop-types'",
    			"",
    			"const ${1} = props => {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			"",
    			"${1}.propTypes = {}",
    			"",
    			"export default ${1}"
    		],
    		"description": "Creates a React Arrow Function Component with ES7 module system with PropTypes"
    	},
    	//React Function Component With Export Default
    	"reactFunctionalComponent": {
    		"key": "reactFunctionalComponent",
    		"prefix": "rfc",
    		"body": [
    			"export default function ${1}() {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			""
    		],
    		"description": "Creates a React Functional Component with ES7 module system"
    	},
    	//React Function Component With Export Default And Prop Types
    	"reactFunctionalComponentWithPropTypes": {
    		"key": "reactFunctionalComponentWithPropTypes",
    		"prefix": "rfcp",
    		"body": [
    			"import PropTypes from 'prop-types'",
    			"",
    			"export default function ${1}(props) {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			"",
    			"${1}.propTypes = {}",
    			""
    		],
    		"description": "Creates a React Functional Component with ES7 module system with PropTypes"
    	},
    	// React Function Component With Separate Export Default
    	"reactFunctionalExportComponent": {
    		"key": "reactFunctionalExportComponent",
    		"prefix": "rfce",
    		"body": [
    			"function ${1}() {",
    			"  return (",
    			"    <div></div>",
    			"  )",
    			"}",
    			"",
    			"export default ${1}"
    		],
    		"description": "Creates a React Functional Component with ES7 module system"
    	}
    }
    ```