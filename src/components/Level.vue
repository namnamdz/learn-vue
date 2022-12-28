<template>
  <div class="level" :id="level">
    <div class="level__header">
      <button class="btn btn--add">Level {{ level }}</button>
      <button class="btn btn--delete" @click="deleteLevel">X ルート削除</button>
      <div class="person__accept" v-for="user in data" :key="user.id">
        <div class="person__info">
          <img
            src="../assets/icons/HN9A8061 1.png"
            alt="avatar"
            class="person__avatar"
          />
          <p class="person__name">{{ user.name }} ({{ user.id }})</p>
        </div>
        <img
          src="../assets/icons/XCircle.png"
          alt="icon delete"
          class="icon_delete"
          @click="deletePerson(user.id)"
        />
      </div>
      <SearchBox
        @handleChangeTextSearch="handleChangeSearchText"
        @handleClickSelectUser="handleClickSelectUser"
        :dataUser="user"
        v-show="true"
      />

      <div class="message__error" v-if="!data.length && isSubmit">
        Level {{ level }} no accept person
      </div>
    </div>
  </div>
</template>

<script>
// import { VueSelect } from "vue-select";
import SearchBox from "./SearchBox.vue";

export default {
  name: "LevelComponent",
  components: {
    SearchBox,
  },
  props: ["data", "id", "user", "level", "isSubmit"],
  setup(props, { emit }) {
    const deleteLevel = () => {
      emit("handleDeleteLevel", props.id);
    };
    const deletePerson = (id) => {
      emit("handleDeletePerson", id);
    };
    const handleChangeSearchText = (searchText) => {
      emit("handleChangeSearchText", searchText);
    };
    const handleClickSelectUser = (idUser) => {
      emit("handleClickSelectUser", idUser);
    };
    return {
      deleteLevel,
      deletePerson,
      handleChangeSearchText,
      handleClickSelectUser,
    };
  },
};
</script>

<style scoped>
.level {
  min-height: 203px;
  transition: 0.5s;
  margin-top: 10px;
}
.btn {
  outline: none;
  cursor: pointer;
  align-items: center;
  border: none;
}
.btn--add {
  width: 88px;
  height: 32px;
  color: #617d98;
  background: #f1f5f8;
  border-radius: 4px;
}
.btn--delete {
  width: 88px;
  height: 32px;
  color: #f86868;
  background: #fff;
  border-radius: 4px;
  margin-left: 35px;
}
.person__accept {
  height: auto;
  display: flex;
  align-items: flex-start;
  margin-top: 8px;
  margin-bottom: 8px;
}
.person__info {
  width: 536px;
  display: flex;
}
.person__avatar {
  width: 40px;
  height: 100%;
}
.person__name {
  margin-left: 10px;
  font-weight: 400;
  font-size: 14px;
}
.icon_delete {
  width: 24px;
  height: 24px;
  margin-top: 8px;
  cursor: pointer;
}
.add_box {
  width: 528px;
  height: 67px;
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
.message__error {
  color: #f86868;
  font-size: 14px;
}
</style>
