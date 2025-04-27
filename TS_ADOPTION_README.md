# Vue TypeScript Adoption

Here is a proof of concept for incrementally adopting TypeScript in a Vue 3 project. The goal is to convert the project to TypeScript gradually, without "boiling the ocean" and rewriting everything at once. This approach allows for a smoother transition and helps to identify potential issues early on.

This project was bootstrapped with `npm create vue@latest` using Vue `3.5.13` and all of the default options in the creation CLI.

### Critical changes

- `eslint.config.ts`
  Added this bit of code:
  ```ts
  import { configureVueProject } from '@vue/eslint-config-typescript'
  configureVueProject({ scriptLangs: ['js', 'ts', 'tsx'] })
  ```
  This allows us to lint both `.js` and `.ts` files in the same project. The `scriptLangs` option is an array of strings that specifies the script languages used in the project. By default, it only includes `ts`, but we can add `js` and `tsx` to support JavaScript and TypeScript with JSX syntax.
- All `.js` files.
  I needed to add a `.d.ts` file to declare the module for the `.js` files that were imported into a `.vue` file using `lang="ts"`. This is necessary because TypeScript needs to know how to handle these files, and by declaring them as modules, we can import them without any issues. One "gotcha" here is that the `.d.ts` files should use absolute paths for their declarations. See `js-helpers.d.ts` for an example.
- Needed to move the main `HelloWorld.vue` component back to a js component by removing the `lang="ts"` attribute from the `<script>` tag. Doing this to simulate a real-world scenario where the root of the project is in JavaScript and we want to incrementally adopt TypeScript.
