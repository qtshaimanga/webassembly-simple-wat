# Web Assembly experiments : s-expression/WAT and Javascript (in web and Node)

Some low-level operations with Web Assembly and Javascript, in the browser and in Node :  
 * calling JS code from WASM (with arg)
 * calling WASM code from JS (with arg)
 * import or export the linear memory space
 * read and write (and share) this memory with JS and WAT/WASM.

## Install, build and run

You first need to install the Web Assembly Binarty Toolkit (WABT) : https://github.com/WebAssembly/wabt

Install dependencies : 

    npm install 

Compile WAT to WASM : 

    wat2wasm simple-wat.wat

This will produce the `simple-wat.wasm` file.  
You can now run it with Node : 

    node simple-wat-node.js

Or in the browser : 

    npm start

## What's in the code ?
The core is in simple-wat.wat : 
 * it imports _displayFunction_ from the host environment (Javascript)
 * it exports the return42 function which just returns 42 (!)
 * it exports the add42To function which add the argument to 42
 * it exports fillMemory which set a value at the beginning of the linear memory space

The linear memory space can be configured in two ways : 
 * through Javascript with WebAssembly.memory() and imported in the WAT/WASM module with `(memory (import "imports" "mem") 1)` 
 * in the WAT/WASM module it self with the `(memory (export "mem") 2)` declaration. As you can see, this memory is exported to the Javascript.

Uncomment the one you want to try, uncomment the other.

The WASM module is instantiated with `WebAssembly.instantiate` in Node, and `WebAssembly.instantiateStreaming` in the browser.