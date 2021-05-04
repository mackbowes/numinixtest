<template>
  <div class="sorterWrap">
    <div class="sorter" @click="open = !open">
      <div class="indicator">
        <span id="sortIndicator">Filter by {{ selected }}</span>
        <img src="../assets/caret-down_minor.png" />
      </div>
      <div class="options" v-if="open">
        <div class="option" @click="setSort('decr')">Name (A-Z)</div>
        <div class="option" @click="setSort('incr')">Name (Z-A)</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Sorter",
  data() {
    return {
      open: false,
      selected: "Name (A-Z)",
    };
  },
  methods: {
    setSort(value) {
      if (value === "decr") {
        this.selected = "Name (A-Z)";
        this.$emit("sortAZ");
      }
      if (value === "incr") {
        this.selected = "Name (Z-A)";
        this.$emit("sortZA");
      }
    },
  },
};
</script>

<style lang="scss">
.sorterWrap {
  position: relative;
}
.sorter {
  display: inline-block;
  border-radius: 8px;
  @media (max-width: 768px) {
    width: auto;
    float: right;
  }
}
.indicator {
  display: flex;
  flex-flow: row;
  align-items: center;
  background-color: white;
  font-family: "Rubik", sans-serif;
  padding: 15px 17px;
  > img {
    padding-left: 5px;
  }
}
.options {
  display: inline-block;
  width: calc(100% - 10px);
  background-color: white;
  font-family: "Rubik", sans-serif;
  padding: 7.5px 5px;
  margin-top: 4px;
  border-radius: 8px;
  position: absolute;
  z-index: 99;
  cursor: pointer;
  box-shadow: -12px 19px 34px -2px #bac9d054;
  @media (max-width: 768px) {
    right: 0;
  }
  > .option {
    display: block;
    padding: 5px 12px;
    &:hover {
      background-color: #f6f6f7;
    }
  }
}
</style>
