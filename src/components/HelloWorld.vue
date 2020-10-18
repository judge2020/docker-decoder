<template>
  <div class="container">
    <h1>{{ msg }}</h1>
    <p>
      This is a tool that decodes your docker `config.json` (used for registry
      authentication) and exposes the credentials that are being used for your
      registries.
      <br />
      This runs entirely on-device - the code is freely available <a href="https://github.com/judge2020/docker-deocder">on GitHub</a> and is hosted on GitHub Pages.
    </p>
    <h3>Paste your entire config.json here.</h3>
    <textarea class="config-input" v-model="config" @input="doMorph(config)">
    </textarea>
    <table class="table">
      <thead>
        <th>Registry</th>
        <th>Username</th>
        <th>Password</th>
      </thead>
      <tbody>
        <tr v-for="auth in auths" v-bind:key="auth.name">
          <td v-text="auth.name" />
          <td v-text="auth.username" />
          <td v-text="auth.password" />
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      config: "",
      auths: [],
    };
  },
  methods: {
    doMorph() {
      this.auths = [];
      let parsed_config = JSON.parse(this.config);
      for (const [key, value] of Object.entries(parsed_config.auths)) {
        let decoded = atob(value["auth"]);
        this.auths.push({
          name: key,
          username: decoded.split(':')[0],
          password: decoded.split(':')[1]
        });
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.config-input {
  width: 50rem;
  height: 15rem;
}
</style>
