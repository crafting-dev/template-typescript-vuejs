# Vue Typescript template for Cloud Sandbox

This is a [Vue](https://vuejs.org/) typescript template, for quick development setup in Cloud Sandbox.

## Specifications

The following `App configuration` was used to create this template:

```yaml
spec:
  endpoints:
  - http:
      routes:
      - backend:
          port: http
          target: ts-vue
        path_prefix: /
    name: app
  services:
  - description: Typescript/Vue template
    name: ts-vue
    workspace:
      checkouts:
      - path: template-typescript-vuejs
        repo:
          git: https://github.com/crafting-dev/template-typescript-vuejs.git
      packages:
      - name: nodejs
        version: ~16
      ports:
      - name: http
        port: 3000
        protocol: HTTP/TCP
```

[Vue-CLI](https://cli.vuejs.org/) was used for standard tooling. To install:

```bash
npm install @vue/cli
```

To test installation:

```bash
npx @vue/cli --version
```

To create template app:
```bash
npx @vue/cli create .
```

* Basic manual settings were selected ([Vue 3] typescript, babel, eslint). See [docs](https://cli.vuejs.org/guide/creating-a-project.html#vue-create) for more details and customization.

To compile and hot-reload for development:
```
npm run serve
```

To compile and minify for production:
```
npm run build
```

To lint and fix files:
```
npm run lint
```

#### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).