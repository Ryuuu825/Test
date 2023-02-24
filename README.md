# Template for SvelteKit with TailwindCSS and Github Pages

```bash
npm init svelte@latest $appname
cd $appname
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init tailwind.config.cjs -p
npm install @sveltejs/adapter-static
```

tailwind.config.cjs

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ['./src/**/*.{html,js,svelte,ts}'],
  theme: {
    extend: {}
  },
  plugins: []
};
```

app.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

svelte.config.js

```js
import adapter from '@sveltejs/adapter-static';
import { vitePreprocess } from '@sveltejs/kit/vite';
const dev = process.argv.includes('dev');

/** @type {import('@sveltejs/kit').Config} */
const config = {
 // Consult https://kit.svelte.dev/docs/integrations#preprocessors
 // for more information about preprocessors
 preprocess: vitePreprocess(),

 kit: {
  adapter: adapter({
   pages: 'build',
   assets: 'build',
   fallback: null,
   precompress: false,
   strict: true,
  }),
  
  paths : {
   base: dev ? '' : {app-name},
  },
  appDir: 'internal',
 }
};

export default config;
```

package.json

```json
{
  "scripts": {
    "dev": "vite dev",
  "build": "vite build",
  "preview": "vite preview",
        [...]
  "deploy": "gh-pages -d build -t true"
 },
  },
  "devDependencies": {
    "@sveltejs/adapter-static": "^1.0.0-next.18",
    "@sveltejs/kit": "next",
    "@tailwindcss/postcss7-compat": "^2.0.2",
    "autoprefixer": "^10.2.4",
    "postcss": "^8.2.4",
    "tailwindcss": "^2.0.2"
  },
  "dependencies": {
    "svelte": "^3.0.0"
  }
}
```

src/routes/layout.js

```js
export const prerender = true;
```

for base url

```js
import { base, assert } from '$app/paths';
```

add a empty file in static folder .nojekyll

reference:

- <https://kit.svelte.dev/docs/adapter-static>
