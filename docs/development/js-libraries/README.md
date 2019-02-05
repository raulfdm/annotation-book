# NPM tips

## package.json

### main (cmj => node)

A CommonJS bundle, suitable for use in Node.js, that requires the external dependency. This corresponds to the "main" field in package.json

### module (esm => ES Modules)

ES module bundle, suitable for use in other people's libraries and applications, that imports the external dependency. This corresponds to the "module" field in package.json

### browser (umd => browser)

a UMD build, suitable for use in any environment (including the browser, as a <script> tag), that includes the external dependency. This corresponds to the "browser" field in package.json

Font: https://github.com/rollup/rollup-starter-lib
