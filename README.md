# docker-decoder

A tool that decodes and displays the logins from the docker config.json file. This won't work if you use a credential helper to store your registry logins (which is why the CLI warns you that logging in without one is dangerous).

Development:

Please don't stage changes to the dist/ folder. This will be done after PR.

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
