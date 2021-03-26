<template>
  <div id="app">
    <Toggler
      v-for="toggler in togglers"
      :key="toggler.content"
      :size="2"
      :checked="checked[toggler.togglerIndex]"
      @updated="updateHandler(toggler.togglerIndex, $event)"
      >{{ toggler.content }}</Toggler
    >
  </div>
</template>

<script>
import Toggler from "./components/Toggler.vue";

export default {
  name: "App",
  components: {
    Toggler,
  },
  data() {
    return {
      checked: [false, false, false],
      // 记录选中的先后次序
      indexes: [],
      togglers: [
        {
          content: "Good",
          togglerIndex: 0,
        },
        {
          content: "Cheap",
          togglerIndex: 1,
        },
        {
          content: "Fast",
          togglerIndex: 2,
        },
      ],
    };
  },
  methods: {
    updateHandler(index, value) {
      if (value === true) {
        // 选中但数组中没有
        this.indexes.push(index);
        // 长度超过 3，删除最前面的
        if (this.indexes.length === 3) {
          this.indexes.shift();
        }
      } else {
        // 没选中但数组中有
        this.indexes.splice(this.indexes.indexOf(index), 1);
      }

      // 遍历 checked 数组
      this.checked = this.checked.map((checked, index) =>
        this.indexes.includes(index) ? true : false
      );
    },
  },
};
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  display: flex;
  flex-direction: column;
}
html,
body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
</style>
