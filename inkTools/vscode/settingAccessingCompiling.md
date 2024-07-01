# Node.js + JavaScript API: Setting up, Accessing Objects, and Compiling ink Code

There is a JavaScript API library named "[inkjs](https://github.com/y-lohse/inkjs)" for working with ink and compiled JSON files. However, this requires the use of a JavaScript runtime such as [Node.js](https://nodejs.org/en).

**Note:** To simplify this material, it will focus on Node.js and its associated tools rather than other every possible JavaScript runtime and package managers.

## Setting Up a Project

Assuming a new or existing NPM project, *inkjs* can be added via the following command:

```bash
npm i inkjs
```

**Note:** For better future-proofing of code, it is highly recommended to use *type: module* with NPM projects.

## Accessing Objects

Once installed, loading the InkJS API consists of two core objects: Story and Compiler. The first creates a new **Story** object based on a JSON file given to it and the second will create a compiled story based on ink code.

A simple example of reading a compiled JSON file and creating a **Story** object would be the following:

```javascript
// Import the readFileSync function from the fs module and the Story class from the inkjs module.
import { readFileSync } from 'fs';
import { Story } from 'inkjs';

// Read the JSON file.
const json = readFileSync('./example.json', 'UTF-8');

// Create a new Story object with the JSON content.
const inkStory = new Story(json);
```

In the previous code, a new **Story** object is created from the compiled JSON file.

## Compiling ink Code

In cases where only the ink code is present, this can be compiled using the **Compiler** object as in the following code.

**Note:** The **Compiler** object is part of the *inkjs/full* module. This includes both **Story** and **Compiler** objects but is much larger than the default inclusion path.

```javascript
// Import the readFileSync and writeFileSync functions from the fs module.
import { readFileSync, writeFileSync } from 'fs';
// For the Compiler class, import the Compiler object from the inkjs/full module.
import { Compiler } from 'inkjs/full';

// Read the ink file.
const ink = readFileSync('./main.ink', 'UTF-8');

// Create a new Compiler object with the ink content.
const compilerObject = new Compiler(ink);

// Compile the ink content to JSON.
// (This will automatically create a Story
//   object internally for immediate playing.)
const compiled = compilerObject.Compile();

// Create compiled JSON.
const jsonBytecode = compiled.ToJson();

// Write the compiled JSON to a file for later playing.
writeFileSync('./main.json', jsonBytecode, 'UTF-8');
```

In the previous example, an ink file is read, compiled, and the resulting JSON output.

Using the [consola](https://www.npmjs.com/package/consola) library, the previous code can also be improved to capture and display any errors encountered during the compilation process.

```javascript
// Import the readFileSync and writeFileSync functions from the fs module.
import { readFileSync, writeFileSync } from 'fs';
// For the Compiler class, import the Compiler object from the inkjs/full module.
import { Compiler } from 'inkjs/full';
// Import consola from the consola module.
import { consola } from "consola";

// Read the ink file.
const ink = readFileSync('./main.ink', 'UTF-8');

// Create a new Compiler object with the ink content.
const compilerObject = new Compiler(ink, {
   errorHandler: (error) => {
       consola.error(error)
   }
});

// Create a variable to store the compiled content.
let compiled = null;

try {
   // Compile the ink content.
   compiled = compilerObject.Compile();
} catch (error) {
   // All errors are caught by the errorHandler.
} finally {
   // Check if there are no errors.
   if(compilerObject.errors.length == 0 && compiled != null) {
       // Print success.
       consola.success('Compiled successfully!');

       // Create compiled JSON.
       const jsonBytecode = compiled.ToJson();
  
       // Write the compiled JSON to a file for later playing.
       writeFileSync('./main.json', jsonBytecode, 'UTF-8');
   }
}
```
