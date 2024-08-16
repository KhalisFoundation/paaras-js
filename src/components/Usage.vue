<template>
  <div class="usage">
    <h4 :id="name">{{name}}</h4>
    <p>{{ description }}</p>
    <code>
        console.assert(
            {{name}}("
            <input type="text" v-model="input" :placeholder=placeholderText() />
            ")
                ===
            <output>'{{ callFn(input) }}'</output>
        );
    </code>
  </div>
</template>

<script>
import * as anvaad from "anvaad-js";

export default {
  name: "Usage",
  props: {
    name: String,
    description: String
  },
  data: () => ({
    input: ""
  }),
  methods: {
    callFn(text) {
      if (this.name.indexOf(".") > -1) {
        const [fn, suffix] = this.name.split(".");
        const passBoolean = (fn === 'unicode' && suffix === 'reverse') // reverse unicode requires a boolean flag
        return anvaad[fn](text, passBoolean ? true : suffix);
      }
      return anvaad[this.name](text);
    },
    placeholderText() {
      const defaultPlaceholder = "Awie imlu gurisK Awie imlu; qU myry gurU ky ipAwry ]";
      if (this.name.indexOf(".") > -1) {
        const suffix = this.name.split(".")[1];
        if (suffix === 'reverse' || suffix === 'unicode') {
          return "ਆਇ ਮਿਲੁ ਗੁਰਸਿਖ ਆਇ ਮਿਲੁ, ਤੂ ਮੇਰੇ ਗੁਰੂ ਕੇ ਪਿਆਰੇ ॥";
        }
        return defaultPlaceholder;
      }
      return defaultPlaceholder;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Mukta+Mahee:wght@200;300;400;500;600;700;800&display=swap');
h3 {
  margin: 40px 0 0;
}
input {
  border: none;
  padding: 5px;
  font-family: "Mukta Mahee", sans-serif;
  font-weight: 200;
  font-style: normal;
}
code {
  font-size: 15px;
  background-color: lightgrey;
  padding: 10px;
  border-radius: 6px;
}
output {
  font-family: "Mukta Mahee", sans-serif;
  font-weight: 400;
  font-style: normal;
}
</style>
