<template>
  <section class="container">
    <div class="code-highlight">
      <pre class="code-pre" v-for="(line, index) in codeLines" :key="index">
      <span class="line-number">{{ index + 1 }}</span>
      <code class="code-line" :class="language" v-html="highlightLine(line)"></code>
    </pre>
      <button class="btn copy-btn" @click="copyToClipboard">Copy</button>
    </div>
  </section>
</template>

<script>
import hljs from 'highlight.js';
import 'highlight.js/styles/github-dark.css'; // Choose the theme you want

export default {
  name: 'CodeHighlight',
  props: {
    code: {
      type: String,
      required: true,
    },
    language: {
      type: String,
      required: true,
    },
  },
  computed: {
    codeLines() {
      return this.code.split('\n');
    },
  },
  methods: {
    highlightLine(line) {
      return hljs.highlight(line, { language: this.language }).value;
    },
    copyToClipboard() {
      const textarea = document.createElement('textarea');
      textarea.textContent = this.code;
      document.body.appendChild(textarea);
      textarea.select();
      document.execCommand('copy');
      document.body.removeChild(textarea);
    },
  },
  mounted() {
    this.$el.querySelectorAll('pre code').forEach((block) => {
      hljs.highlightBlock(block);
    });
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 94.75vh;
  width: 90vw;
  margin: auto;
}
.code-highlight {
  padding: 1rem 0.75rem;
  padding-bottom: 2.5rem;
  font-size: 16px;
  /* width: 90%; */
  border: 1px solid #fff;
  border-radius: 1rem;
  position: relative;
  height: 95%;
  overflow: scroll;
  width: 100%;
}

.code-pre {
  height: 1.5rem;
  display: flex;
  gap: 1.5rem;
}

.line-number {
  display: inline;
  width: 2em;
  text-align: right;
  color: #888;
}

.code-line {
  display: inline;
  margin-left: 2rem;
  padding: 0;
  margin: 0;
  background-color: transparent;
}

.copy-btn {
  position: sticky;
  /* sticky: bottom; */
  /* position: -webkit-sticky; */
  bottom: 0;
  left: 8px;
  right: 8px;
  transform: translate(0, 100%);
  padding: 8px 24px;
  color: #fff;
  background-color: #ffffff22;
  border-radius: 8px;
  cursor: pointer;
  margin-left: 88%;
  filter: opacity(0);
  transition: all 0.25s ease-in-out;
}

.code-highlight:hover .copy-btn {
  filter: opacity(1);
}

/* Modern-looking scrollbar for webkit-based browsers */
::-webkit-scrollbar {
  width: 8px; /* adjust as needed */
  height: 8px; /* adjust as needed */
}

::-webkit-scrollbar-track {
  background: transparent;
}

::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.2);
  border-radius: 10px;
  border: 1px solid rgba(0, 0, 0, 0.1);
}

/* Modern-looking scrollbar for Firefox */
::-moz-scrollbar {
  width: 8px; /* adjust as needed */
  height: 8px; /* adjust as needed */
}

::-moz-scrollbar-track {
  background: transparent;
}

::-moz-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.2);
  border-radius: 10px;
  border: 1px solid rgba(0, 0, 0, 0.1);
}
</style>
