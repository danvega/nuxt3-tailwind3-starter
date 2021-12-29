# Nuxt 3 + Tailwind CSS 3 Starter

This is a minimal starter template for Nuxt 3 projects with Tailwind CSS 3. It includes a simple template `pages/index.vue` and a Tailwind UI example component in `pages/features.vue`. To make the Tailwind UI component work this setup includes [heroicons](https://heroicons.com/). You can either clone this repo or use the steps below to to create a new Nuxt 3 + Tailwind CSS 3 project.

## Steps

Start by creating a new Nuxt 3 project named `hello-tailwind-3` with the following command:

`npx nuxi init hello-tailwind-3`

Install Tailwind CSS as a development dependency with the following command:

- `npm install -D tailwindcss`

Create your `tailwind.config.js` file with the following content:

- `npx tailwindcss init`

Open up `tailwind.config.js` and add the paths to all of your template files under content:

```javascript
module.exports = {
  content: [
    "./components/**/*.{js,vue,ts}",
    "./layouts/**/*.vue",
    "./pages/**/*.vue",
    "./plugins/**/*.{js,ts}",
    "./nuxt.config.{js,ts}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Create a new file `assets/css/tailwind.css` and add the following add the @tailwind directives for each of Tailwind’s layers:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Open up `nuxt.config.js` and add the following:

```javascript
import { defineNuxtConfig } from 'nuxt3'

// https://v3.nuxtjs.org/docs/directory-structure/nuxt.config
export default defineNuxtConfig({
  build: {
    postcss: {
      postcssOptions: {
        plugins: {
          tailwindcss: {},
          autoprefixer: {},
        },
      },
    },
  },
  css: [
    "~/assets/css/tailwind.css"
  ],
})
```

If you want to learn more about what the code above is doing visit the [documentation](https://v3.nuxtjs.org/docs/directory-structure/nuxt.config#css). The css option will allow you to define a css file that you want to set globally and include in any page.

## Vue Templates

To get started you will need to remove `app.vue` and create a new page `pages/index.vue` with the following content:

```vue
<template>
  <div class="container mx-auto bg-gray-300 p-8">
    <h1 class="font-bold text-gray-600 text-lg">Hello, Tailwind 3!</h1>
  </div>
</template>
```

If you start the app with `npm run dev` you should be able to visit http://localhost:3000/ and see the page you just created along with Tailwind 3 in action.

### Tailwind UI

I also included a [Tailwind UI](https://tailwindui.com/components/marketing/sections/feature-sections) example component in `pages/features.vue` which you can use to test out your Tailwind CSS 3 configuration. To use this example component you will need to install the following dependencies:

```bash
npm install @heroicons/vue
```

Create `pages/features.vue` with the following content:

```vue
<template>
  <div class="py-12 bg-white">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="lg:text-center">
        <h2 class="text-base text-indigo-600 font-semibold tracking-wide uppercase">Transactions</h2>
        <p class="mt-2 text-3xl leading-8 font-extrabold tracking-tight text-gray-900 sm:text-4xl">
          A better way to send money
        </p>
        <p class="mt-4 max-w-2xl text-xl text-gray-500 lg:mx-auto">
          Lorem ipsum dolor sit amet consect adipisicing elit. Possimus magnam voluptatum cupiditate veritatis in accusamus quisquam.
        </p>
      </div>

      <div class="mt-10">
        <dl class="space-y-10 md:space-y-0 md:grid md:grid-cols-2 md:gap-x-8 md:gap-y-10">
          <div v-for="feature in features" :key="feature.name" class="relative">
            <dt>
              <div class="absolute flex items-center justify-center h-12 w-12 rounded-md bg-indigo-500 text-white">
                <component :is="feature.icon" class="h-6 w-6" aria-hidden="true" />
              </div>
              <p class="ml-16 text-lg leading-6 font-medium text-gray-900">{{ feature.name }}</p>
            </dt>
            <dd class="mt-2 ml-16 text-base text-gray-500">
              {{ feature.description }}
            </dd>
          </div>
        </dl>
      </div>
    </div>
  </div>
</template>

<script>
import { AnnotationIcon, GlobeAltIcon, LightningBoltIcon, ScaleIcon } from '@heroicons/vue/outline'

const features = [
  {
    name: 'Competitive exchange rates',
    description:
      'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Maiores impedit perferendis suscipit eaque, iste dolor cupiditate blanditiis ratione.',
    icon: GlobeAltIcon,
  },
  {
    name: 'No hidden fees',
    description:
      'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Maiores impedit perferendis suscipit eaque, iste dolor cupiditate blanditiis ratione.',
    icon: ScaleIcon,
  },
  {
    name: 'Transfers are instant',
    description:
      'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Maiores impedit perferendis suscipit eaque, iste dolor cupiditate blanditiis ratione.',
    icon: LightningBoltIcon,
  },
  {
    name: 'Mobile notifications',
    description:
      'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Maiores impedit perferendis suscipit eaque, iste dolor cupiditate blanditiis ratione.',
    icon: AnnotationIcon,
  },
]

export default {
  setup() {
    return {
      features,
    }
  },
}
</script>
```

If you start the app with `npm run dev` you should be able to visit http://localhost:3000/features and see the page you created with Tailwind UI.
