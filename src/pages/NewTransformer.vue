<template>
	<div class="p-grid">
		<prism-editor
      class="my-editor height-300"
      v-model="code"
      :highlight="highlighter"
      :line-numbers="lineNumbers"></prism-editor>
	</div>
</template>

<script>
// import highlighting library (you can use any library you want just return html string)
import { highlight, languages } from 'prismjs/components/prism-core';
import 'prismjs/components/prism-clike';
import 'prismjs/components/prism-java';
import 'prismjs/themes/prism-tomorrow.css'; // import syntax highlighting styles

const bootCode = `
public class HelloWorld {
	public static void main(String[] args) {
		System.out.println("Hello World!");
	}
}
`;

export default {
	components: {
  //  PrismEditor,
  },
  data: () => ({
		code: bootCode.trim(),
		lineNumbers: true
	}),
  methods: {
    highlighter(code) {
      return highlight(code, languages.java); //returns html
    },
  }
}
</script>

<style scoped lang="scss">
	/* required class */
  .my-editor {
    /* we dont use `language-` classes anymore so thats why we need to add background and text color manually */
    background: #2d2d2d;
    color: #ccc;

    /* you must provide font-family font-size line-height. Example: */
    font-family: Fira code, Fira Mono, Consolas, Menlo, Courier, monospace;
    font-size: 14px;
    line-height: 1.5;
    padding: 25px 10px;
  }
</style>

<style lang="scss">
	/* optional class for removing the outline */
	.prism-editor__textarea:focus {
		outline: none;
	}
</style>
