<template>
  <div class="dropdown-wrap" :class="classes">
    <button class="dropdown-button dropdown-toggle primary" 
      @click="focus">
      {{text}}
      <span class="caret"></span>
    </button>
    <div class="mask" @click="blur"></div>
    <div class="dropdown-menu">
      <div class="dropdown-header" v-if="$slots.default">
        <slot></slot>
      </div>
      <div class="dropdown-menu-item" 
        v-for="(item, index) in reformedList" 
        :key="index" 
        :class="item.type"
        @click="itemSelect(item, index)">
        {{item.text}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "dropdown",
  data() {
    return {
      show: false
    };
  },
  methods: {
    itemSelect(item, index) {
      this.$emit("select", {
        item,
        index,
        next: () => {
          this.show = false;
        }
      });
      if (this.autoBlur) {
        this.show = false;
      }
    },
    blur(event) {
      this.show = false;
      this.$emit("blur");
    },
    focus() {
      if (!this.disabled) {
        this.show = true;
        this.$emit("focus");
      }
    }
  },
  computed: {
    reformedList() {
      return this.list.map(item => {
        if (typeof item === "object") {
          return {
            text: item.text,
            type: item.type
          };
        } else {
          return {
            text: item,
            type: "text"
          };
        }
      });
    },
    classes() {
      return {
        open: this.show,
        disabled: this.disabled
      };
    }
  },
  props: {
    list: {
      required: true,
      default: function() {
        return [];
      }
    },
    text: {
      default: "button",
      type: String
    },
    disabled: {
      default: false,
      type: Boolean
    },
    autoBlur: {
      type: Boolean,
      default: true
    }
  }
};
</script>
<style lang="less" scoped>
.dropdown-wrap {
  display: inline-block;
  vertical-align: middle;
  position: relative;
  &.disabled {
    .dropdown-button {
      border-color: #7e8a9a !important;
      background-color: #92a2b9 !important;
      cursor: not-allowed;
      &:focus {
        box-shadow: none;
      }
    }
  }
  * {
    box-sizing: border-box;
  }
  &.open {
    .dropdown-button {
      color: #fff;
      background-color: #545b62;
      border-color: #4e555b;
    }
    .dropdown-menu {
      display: block;
    }
    .mask {
      display: block;
      z-index: 1;
    }
  }
  .dropdown-button {
    display: inline-block;
    font-weight: 400;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    user-select: none;
    border: 1px solid transparent;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: 0.25rem;
    transition: all 0.15s ease-in-out;
    &.primary {
      color: #fff;
      background-color: #6c777f;
      border-color: #6c777f;
    }
    &:focus {
      outline: 0;
      box-shadow: 0 0 0 0.2rem rgba(108, 117, 125, 0.5);
    }
    &::after {
      display: inline-block;
      width: 0;
      height: 0;
      margin-left: 0.25em;
      vertical-align: 0.25em;
      content: "";
      border-top: 0.25em solid;
      border-right: 0.25em solid transparent;
      border-bottom: 0;
      border-left: 0.25em solid transparent;
    }
  }
  .mask {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
  }
  .dropdown-menu {
    position: absolute;
    top: 100%;
    left: 0;
    z-index: 1000;
    display: none;
    float: left;
    min-width: 10rem;
    padding: 0.5rem 0;
    margin: 0.125rem 0 0;
    font-size: 1rem;
    color: #212121;
    text-align: left;
    list-style: none;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid rgba(0, 0, 0, 0.15);
    border-radius: 0.25rem;
    .dropdown-header {
      display: block;
      padding: 0.5rem 1.5rem;
      margin-bottom: 0;
      font-size: 0.875rem;
      color: #6c777f;
      white-space: nowrap;
    }
    .dropdown-menu-item {
      display: block;
      width: 100%;
      padding: 0.25rem 1.5rem;
      clear: both;
      font-weight: 400;
      color: #212121;
      text-align: inherit;
      white-space: nowrap;
      background-color: transparent;
      border: 0;
      &:hover {
        color: #2b2b2b;
        text-decoration: none;
        background-color: #f1f9f7;
      }
      &:active {
        color: #fff;
        text-decoration: none;
        background-color: #007bff;
      }
      &.divider {
        height: 0;
        margin: 0.5rem 0;
        overflow: hidden;
        border-top: 1px solid #e9ecef;
        &:hover {
          background-color: #fff;
        }
        &:active {
          background-color: #fff;
        }
      }
      &.text {
      }
    }
  }
}
</style>
