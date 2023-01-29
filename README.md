# Test

```bash
npm init svelte@latest {app-name}
cd {app-name}
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init tailwind.config.cjs -p
npm install svelte
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

src/routes/layout.js
```js
export const prerender = true;
```

for base url
```js
import { base, assert } from '$app/paths';

```


reference:
- https://kit.svelte.dev/docs/adapter-static