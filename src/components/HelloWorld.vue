<template>
  <div>
    <div
      ref="aaa"
      :style="{
        height: `${containerHeight}px`,
        overflow: 'auto',
        boxSizing: 'border-box'
      }"
      @scroll="onScroll"
    >
      <div
        :style="{
          paddingTop: `${startOffset}px`,
          paddingBottom: `${endOffset}px`
        }"
      >
        <div
          v-for="(content, i) in renderList"
          :key="i"
          :style="{ height: `${itemHeight}px` }"
        >
          {{ content }}
        </div>
      </div>
    </div>
    {{}}
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  xStart = 0;
  containerHeight = 200;
  itemHeight = 100;
  dataSize = 1000;
  bufferSize = 1;

  list = new Array(1000).fill(0).map((_, i) => `this is content ${i}`);

  mounted() {
    console.log();
  }

  get contentHeight() {
    return this.dataSize * this.itemHeight;
  }

  get startIndex() {
    return Math.max(0, this.xStart - Math.ceil(this.viewSize * 0.5));
  }

  get endIndex() {
    return Math.min(
      this.dataSize,
      this.startIndex + this.viewSize + Math.ceil(this.viewSize * 1.5)
    );
  }

  get renderList() {
    return this.list.slice(this.startIndex, this.endIndex);
  }

  get viewSize() {
    return this.containerHeight / this.itemHeight;
  }

  get startOffset() {
    return this.startIndex * this.itemHeight;
  }

  get endOffset() {
    return this.contentHeight - this.endIndex * this.itemHeight;
  }

  onScroll(event: ScrollEvent) {
    const currentIdx = Math.floor(event.target.scrollTop / this.itemHeight);
    this.xStart = currentIdx;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
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
</style>
