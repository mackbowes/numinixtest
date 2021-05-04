<template>
  <div class="userCard">
    <div
      class="userImage"
      @mouseover="setModal(true)"
      @mouseleave="setModal(false)"
    >
      <div class="userMenu" v-if="imageHovered === true">
        <div class="userMenuButtonRow">
          <div class="editButton" @click="shruggie">Edit</div>
          <div class="viewButton" @click="shruggie">View</div>
        </div>
      </div>
      <img :src="image" />
    </div>
    <div class="userCardContent">
      <h3 class="userName">{{ fullName }}</h3>
      <h4 class="userAt">@{{ username }}</h4>
      <div class="userCatchPhrase">{{ catchPhrase }}</div>
      <div class="userDetailList">
        <div class="listItem" name="email">
          <img src="../assets/mail.png" />
          <span>{{ email }}</span>
        </div>
        <div class="listItem" name="location">
          <img src="../assets/pin.png" />
          <span
            >{{ street }}, {{ suite }}, {{ city }}, {{ zipcode }}, {{ lat }},
            {{ lng }}</span
          >
        </div>
        <div class="listItem" name="phone">
          <img src="../assets/phone.png" />
          <span>{{ phone }}</span>
        </div>
        <div class="listItem" name="website">
          <img src="../assets/globe.png" />
          <span>{{ website }}</span>
        </div>
        <div class="listItem" name="bizName">
          <img src="../assets/work.png" />
          <span>{{ bizName }}</span>
        </div>
        <div class="listItem" name="biz">
          <img src="../assets/building.png" />
          <span>{{ biz }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserCard",
  props: [
    "fullName",
    "username",
    "image",
    "catchPhrase",
    "email",
    "street",
    "suite",
    "zipcode",
    "city",
    "lat",
    "lng",
    "phone",
    "website",
    "biz",
    "bizName",
  ],
  data() {
    return {
      imageHovered: "",
    };
  },
  methods: {
    setModal(value) {
      this.imageHovered = value;
    },
    shruggie() {
      window.alert("didn't know what you wanted me to do here");
    },
  },
};
</script>

<style lang="scss">
.userCard {
  display: flex;
  width: calc(363 / 1976 * 100vw);
  height: 725px;
  border-radius: 8px;
  background-color: white;
  flex-flow: column nowrap;
  @media (max-width: 768px) {
    display: block;
    width: auto;
    height: auto;
    padding: 20px;
  }
}
.userImage {
  display: block;
  width: calc(363 / 1976 * 100vw);
  height: 289px;
  border-radius: 8px 8px 0 0;
  overflow: hidden;
  position: relative;
  @media (max-width: 768px) {
    width: 33%;
    float: right;
    border-radius: 8px;
  }
  img {
    display: block;
    width: 100%;
    margin: 0;
    border-radius: 8px 8px 0 0;
    @media (max-width: 768px) {
      border-radius: 8px;
    }
  }
  .userMenu {
    @media (max-width: 768px) {
      display: none;
    }
    position: absolute;
    background-color: rgba(0, 0, 0, 0.27);
    width: 100%;
    height: 100%;
    display: grid;
    place-items: center;
    .userMenuButtonRow {
      display: flex;
      flex-flow: row;
      font-family: "Rubik", sans-serif;
      .editButton {
        padding: 8px 16px;
        display: grid;
        place-items: center;
        color: #1575bf;
        background-color: white;
        border-radius: 4px;
        margin-right: 8px;
        cursor: pointer;
      }
      .viewButton {
        padding: 8px 16px;
        display: grid;
        place-items: center;
        color: white;
        background-color: #1575bf;
        border-radius: 4px;
        cursor: pointer;
      }
    }
  }
}
.userCardContent {
  margin: 25px 28px;
  @media (max-width: 768px) {
    margin: 0;
  }
  h3 {
    font-family: "Rubik", sans-serif;
    font-weight: 500;
    font-size: 24px;
    line-height: 28px;
    margin: 0;
    @media (max-width: 768px) {
      font-size: 18px;
    }
  }
  h4 {
    font-family: "Rubik", sans-serif;
    font-weight: 400;
    font-size: 1rem;
    line-height: 25px;
    margin: 0;
    color: #909090;
    @media (max-width: 768px) {
      font-size: 13px;
    }
  }
  .userCatchPhrase {
    margin: 15px 0 27.5px 0;
    color: #51c5ff;
    font-family: "Rubik", sans-serif;
    font-weight: 400;
    font-size: 1rem;
    line-height: 25px;
    @media (max-width: 768px) {
      font-size: 13px;
    }
  }
  .userDetailList {
    .listItem {
      display: flex;
      flex-flow: row nowrap;
      align-items: flex-start;
      margin-bottom: 12px;
      > img {
        width: 20px;
        margin-top: 5px;
        @media (max-width: 768px) {
          width: 13px;
        }
      }
      > span {
        font-family: "Rubik", sans-serif;
        margin-left: 1rem;
        font-size: 1rem;
        line-height: 25px;
        @media (max-width: 768px) {
          font-size: 13px;
        }
      }
    }
  }
}
</style>
