<template>
  <div>
    <div class="add_box">
      <p class="title">承認者の追加</p>
      <div class="search__box">
        <img
          src="../assets/icons/search.png"
          alt="search_icon"
          class="search_icon"
        />
        <input
          type="text"
          class="input_search"
          placeholder="氏名や社員番号で検索する"
          v-model="textSearch"
          @input="handleChangeTextSearch"
          @click="handleClick"
        />
      </div>
    </div>
    <div class="box" v-show="this.showDropdown">
      <div class="box__data">
        <div
          class="user"
          @click="handleClickSelectUser(user.id)"
          v-for="user in dataUser"
          :key="user.id"
        >
          {{ user.name }} {{ user.id }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchBox",
  props: ["dataUser"],
  data() {
    return {
      textSearch: "",
      showDropdown: false,
    };
  },
  methods: {
    handleChangeTextSearch() {
      this.$emit("handleChangeTextSearch", this.textSearch);
    },
    handleClickSelectUser(id) {
      this.$emit("handleClickSelectUser", id);
      //clear the serach field
      this.textSearch = "";
      // close the dropdown
      this.showDropdown = false;
    },
    handleClick() {
      this.showDropdown = true;
    },
  },
};
</script>

<style scoped>
.add_box {
  width: 528px;
  margin-top: 8px;
}
.search__box {
  width: 528px;
  height: 39px;
  display: flex;
  align-content: flex-start;
  border: 1px solid #dcdcdc;
  border-radius: 4px;
  margin-top: 8px;
}
.search_icon {
  height: 24px;
  width: 24px;
  top: 7.5px;
  margin-left: 10px;
  margin-top: 6px;
}
.input_search {
  width: 80%;
  height: 30px;
  outline: none;
  border: none;
  margin-left: 10px;
  margin-top: 3px;
  font-weight: 400;
  font-size: 14px;
}
.box {
  margin-top: 8px;
  margin-bottom: 10px;
}
.box__data {
  width: 528px;
  background: #f1f5f8;
  height: 150px;
  overflow-y: scroll;
}
.user {
  width: 100%;
  height: 30px;
  cursor: pointer;
}
.box__data:hover {
  padding-left: 0px;
}
.user:hover {
  background: #fff;
}
</style>
