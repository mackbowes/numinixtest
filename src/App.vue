<template>
  <div class="pageWrap">
    <div class="nav"></div>
    <div class="innerContent">
      <div class="searchSortRow">
        <div class="search">
          <SearchBar @runQuery="filterUsers"></SearchBar>
        </div>
        <div class="sort">
          <Sorter @sortAZ="sort('decr')" @sortZA="sort('incr')"></Sorter>
        </div>
      </div>
      <div class="cardGrid">
        <UserCard
          v-for="(user, index) in filteredUsers"
          :key="index"
          v-bind="user"
          :catchPhrase="user.company.catchPhrase"
          :bizName="user.company.name"
          :biz="user.company.bs"
          :street="user.address.street"
          :suite="user.address.suite"
          :zipcode="user.address.zipcode"
          :city="user.address.city"
          :lat="user.address.geo.lat"
          :lng="user.address.geo.lng"
        ></UserCard>
      </div>
    </div>
  </div>
</template>

<script>
//import HelloWorld from "./components/HelloWorld.vue";
import UserCard from "./components/UserCard.vue";
import Sorter from "./components/Sorter.vue";
import SearchBar from "./components/Searcher.vue";

import axios from "axios";

export default {
  name: "App",
  mounted() {
    let inside = this;

    axios.get("http://jsonplaceholder.typicode.com/users").then((res) => {
      inside.users_data = res.data;
      inside.users_data.map((user) => {
        user.fullName = user.name;
        delete user.name;
        user.image = `https://picsum.photos/seed/${user.username}/350`;
      });
    });
  },
  data() {
    return {
      users_data: [],
      query: "",
    };
  },
  methods: {
    sort(direction) {
      this.users_data.sort((a, b) => {
        if (direction === "decr") {
          if (a.fullName < b.fullName) {
            return -1;
          }
          if (a.fullName > b.fullName) {
            return 1;
          }
          return 0;
        }
        if (direction === "incr") {
          if (a.fullName > b.fullName) {
            return -1;
          }
          if (a.fullName < b.fullName) {
            return 1;
          }
          return 0;
        }
      });
    },
    filterUsers(val) {
      this.query = val;
    },
  },
  computed: {
    filteredUsers() {
      if (this.query === "") {
        return this.users_data;
      } else {
        let newUsers = this.users_data.filter((user) => {
          let query = this.query.toUpperCase();
          let string = JSON.stringify(user);
          if (string.toUpperCase().includes(query)) {
            return true;
          }
        });
        return newUsers;
      }
    },
  },
  components: {
    //    HelloWorld,
    UserCard,
    Sorter,
    SearchBar,
  },
};
</script>

<style lang="scss">
.pageWrap {
  display: flex;
  flex-flow: column nowrap;
  width: 100vw;
  min-height: 100vh;
  justify-content: flex-start;
  background-color: #f2f5fa;
}
.nav {
  display: block;
  height: calc(91 / 1976 * 100vh);
  background-color: white;
  box-shadow: 9px 6px 24px -2px #0000000f;
}

.searchSortRow {
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;
  margin-top: calc(78 / 1976 * 100vh);
  margin-bottom: calc(100 / 1976 * 100vh);
  @media (max-width: 768px) {
    flex-flow: column wrap;
  }
}

.innerContent {
  display: flex;
  flex-flow: column nowrap;
  margin: 0 calc(167 / 1917 * 100vw);
}
.cardGrid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  column-gap: calc(43.5 / 1917 * 100vw);
  row-gap: calc(65 / 1976 * 100vh);
  @media (max-width: 768px) {
    grid-template-columns: 1fr;
  }
}
</style>
