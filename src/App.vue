<template>
  <!-- <h3>Cheatly your cheating buddy!!!</h3> -->
  <CodeList :list="codeObj" @codeChange="handleCodeChange" />
  <CodeHighlight :code="sampleCode" :language="lang" />
</template>

<script>
import CodeHighlight from './components/CodeHighlight.vue';
import CodeList from './components/CodeList.vue';
import codeObj from './assets/codeObj.js';

export default {
  components: {
    CodeHighlight,
    CodeList,
  },
  data() {
    return {
      codeObj: codeObj,
      currentId: 1,
    };
  },
  computed: {
    sampleCode() {
      return this.codeObj[this.currentId - 1].code;
    },
    lang() {
      return this.codeObj[this.currentId - 1].lang;
    },
  },
  methods: {
    handleCodeChange(id) {
      this.currentId = id;
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  background: #141e30; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    315deg,
    #243b55,
    #141e30
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    315deg,
    #243b55,
    #141e30
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}

.btn {
  border: none;
  background-color: transparent;
  font-size: 1rem;
}
</style>
