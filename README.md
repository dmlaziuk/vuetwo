Vue Sample
==========

### Description
The aim of this project is to use Vue.js framework with Ruby on Rails.

[Reference tutorial](https://github.com/multpix/rails-webpacker-vue)

### Dependencies
- node 9.4
- yarn 1.3
- webpacker 3.2
- vue 2.5
- ruby 2.4
- rails 5.1

### Initializing process
```
$ rails new vuetwo --webpack=vue
$ cd vuetwo
$ cat > Procfile.dev <<END_CONF
rails: bundle exec rails s
# watch: ./bin/webpack-watcher
wpack: ./bin/webpack-dev-server
END_CONF
$ cd bin
$ cat > server <<END_CONF
#!/bin/bash -i
bundle exec foreman start -f Procfile.dev
END_CONF
$ chmod +x ./server
$ cd ..
$ rails g controller hello index
```
Modify `routes.rb`:
```
root ‘hello#index’
```

Create `app/javascript/packs/app.js`:
```js
import Vue from 'vue/dist/vue.esm'
import App from '../components/app.vue'

document.addEventListener('DOMContentLoaded', () => {
  const app = new Vue({
    el: '#app',
    data: {
      message: "Can you say hello?"
    },
    components: { App }
  })
})
```

Create `app/javascript/components/app.vue`:
```erb
<template>
  <div id="app">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      message: "Hello Vue!"
    }
  }
}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}
</style>
```

Modify `app/views/layouts/application.html.erb` with `stylesheet_pack_tag` set to `'app'` and `javascript_pack_tag` set to `'app'`:
```erb
<!DOCTYPE html>
<html>
  <head>
    <title>Vuetwo</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag 'application', media: 'all' %>
    <%= stylesheet_pack_tag 'app' %>
    <%= javascript_include_tag 'application' %>
    <%= javascript_pack_tag 'app' %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```
Modify `app/views/hello/index.html.erb`:
```erb
<div id="app">
    <p>{{ message }}</p>
    <app/>
</div>
```

### Runing app
```
$ ./bin/server
```
Open it in browser [localhost:5000](localhost:5000).
