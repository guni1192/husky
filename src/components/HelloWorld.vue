<template>
  <div id="md-editor">
    <div id="edit-field">
      <textarea id="md-editor" v-model="text"></textarea>
    </div>
    <div id="preview-field">
      <article class="markdown-body">
        {{ text }}
      </article>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      text: ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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

#md-editor {
  background-color: #00FF00;
  display: flex;
  flex: auto;
  justify-content: center;/* 3 */
  align-items: center;    /* 4 */
}

#edit-field {
  background-color: #FFF000;
  margin: 0 10px;
}

#preview-field {
  background-color: #FF0000;
  margin: 0 10px;
}

</style>
