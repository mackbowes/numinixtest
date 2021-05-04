<template>
  <div class="searchWrap">
    <img src="../assets/Search.png" />
    <input
      type="text"
      class="search"
      placeholder="Find Customers"
      v-model="query"
      @input="emitData(query)"
    />
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  data() {
    return {
      query: "",
    };
  },
  methods: {
    emitData($data) {
      this.$emit("runQuery", $data);
    },
  },
};
</script>

<style lang="scss">
.searchWrap {
  display: flex;
  width: calc(546 / 1917 * 100vw);
  background-color: white;
  flex-flow: row;
  padding: 15px 17px;
  font-family: "Rubik", sans-serif;
  line-height: 25px;
  border-radius: 8px;
  @media (max-width: 768px) {
    width: auto;
    margin-bottom: 1rem;
  }
  ::placeholder {
    color: black;
  }
  > img {
    margin-right: 1rem;
  }
  > input {
    border: 0;
    outline: none;
    font-size: 1rem;
    display: block;
    width: 100%;
  }
}
</style>
