<template>
  <div id="app">
    <p>选中对象{{item}};index:{{index}}</p>
    <p>
      <Dropdown class="demo-item" 
        text="简单下拉框" 
        :list="list1" 
        @select="select"
      ></Dropdown>
      <Dropdown class="demo-item" 
        text="过滤横线" 
        :list="list2"
        @select="selectFilter"
        :auto-blur="false"
      ></Dropdown>
      <Dropdown class="demo-item" 
        text="不可选中" 
        :list="list3" 
        @select="select"
        :disabled="true"
      ></Dropdown>
      <Dropdown class="demo-item" 
        text="使用header插槽" 
        :list="list3" 
        @select="select"
      >
        <div>
          dropdown header
        </div>
      </Dropdown>
    </p>
  </div>
</template>

<script>
import Dropdown from "./components/Dropdown.vue";

export default {
  name: "App",
  data() {
    return {
      index: null,
      item: null,
      list1: ["A", "B", "C"],
      list2: ["A", { type: "divider" }, "B", "C"],
      list3: ["A", { type: "divider" }, "B", "C", { type: "divider" }, "D"]
    };
  },
  methods: {
    select({ item, index }) {
      this.item = item;
      this.index = index;
    },
    selectFilter({ item, index, next }) {
      if (item.type !== "divider") {
        next();
      }
    }
  },
  components: {
    Dropdown
  }
};
</script>

<style>
body {
  font-size: 16px;
}
#app {
  p {
    color: #333;
  }
}
.demo-item {
  margin-right: 0.35rem;
}
</style>
