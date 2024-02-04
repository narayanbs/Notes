- Install Tailwind using npm and create tailwind.config.js
```bash
npm install -D tailwindcss
npx tailwindcss init
```

- create build, src directories
- Configure template path in your tailwind.config.js 
```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{html,js}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
- create src/input.css and add the following
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
- Start the build process. It scans the template files for classes and build your css
```
npx tailwindcss -i ./src/input.css -o ./build/output.css --watch
```
- Add the compiled css to our html
```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="/build/output.css" rel="stylesheet">
</head>
<body>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</body>
</html>
```