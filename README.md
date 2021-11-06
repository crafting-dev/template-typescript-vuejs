# Typescript/Vuejs template for Crafting Sandbox

This is a Typescript/[Vue.js](https://vuejs.org/) template, configured for quick development setup in [Crafting Sandbox](https://crafting.readme.io/docs).

## Specifications

This template contains a single [`Ping`](src/components/Ping.vue) component:
```vue
<template>
  <Ping />
</template>
```

This component consists of a form with a single input and a button. 
```vue
<form @submit.prevent="pingServer">
  <input v-model="ping" placeholder="Ping server with some text...">
  ...
  <button type="submit">Submit</button>
</form>
```
Once form is submitted, a GET request is made to some backend server that exposes a `/ping` api. This Ping component then renders the api response data.
```vue
<div v-if="pong">
  <code>
    {{
      JSON.stringify({
        "ping": pong.ping,
        "received_at": new Date(pong.received_at).toLocaleString()
      }, null, 2)
    }}
  </code>
</div>
```

To run the app, you can do:
```bash
npm start -- --port 3001
```

## App Configuration

The following [App configuration](https://crafting.readme.io/docs/app-spec) was used to create this template:

```yaml
endpoints:
- http:
    routes:
    - backend:
        port: http
        target: ts-vue
      path_prefix: /
  name: app
services:
- description: Typescript/Vuejs template
  name: ts-vue
  workspace:
    checkouts:
    - path: src/template-typescript-vuejs
      repo:
        git: https://github.com/crafting-dev/template-typescript-vuejs.git
    packages:
    - name: nodejs
      version: ~16
    ports:
    - name: http
      port: 3001
      protocol: HTTP/TCP
```
