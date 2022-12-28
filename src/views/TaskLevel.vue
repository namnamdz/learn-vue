<template>
  <div class="container" id="id">
    <span class="title">承認ルート</span>
    <br />
    <button class="btn__create" @click="hanldeAddLevel">
      <img src="../assets/icons/Plus.png" alt="plus" class="plus__icon" />
      ルートの追加
    </button>
    <p class="error__message" v-show="this.errorMessage">
      {{ this.errorMessage }}
    </p>
    <div>
      <LevelVue
        :data="level.employees"
        :id="level.id"
        :user="user"
        :level="level.level"
        @handleDeleteLevel="handleDeleteLevel"
        @handleDeletePerson="handleDeleConfirmPerson($event, level.level)"
        @handleClickSelectUser="handleClickSelectUser($event, level.level)"
        :isSubmit="isSubmit"
        v-for="level in data"
        :key="level.level"
        class="level"
      />
    </div>
    <button class="btn btn__create" @click="handleSubmit">Submit</button>
  </div>
</template>

<script>
import LevelVue from "../components/Level.vue";
export default {
  name: "TaskLevel",
  components: {
    LevelVue,
  },
  data() {
    return {
      errorMessage: "",
      errorEmpty: [],
      data: [
        {
          id: 1,
          level: 1,
          employees: [
            { name: "Person1", id: 122222 },
            { name: "Person1", id: 122283 },
            { name: "Person1", id: 122284 },
          ],
        },
        {
          id: 2,
          level: 2,
          employees: [{ name: "Person1", id: 13333 }],
        },
        {
          id: 3,
          level: 3,
          employees: [{ name: "Person1", id: 1113131 }],
        },
        {
          id: 4,
          level: 4,
          employees: [],
        },
      ],
      user: [
        {
          name: "Person1",
          id: "1",
        },
        {
          name: "Person1",
          id: "12",
        },
        {
          name: "Person1",
          id: "3",
        },
        {
          name: "Person1",
          id: "4",
        },
        {
          name: "Person1",
          id: "5",
        },
        {
          name: "Person1",
          id: "6",
        },
        {
          name: "Person1",
          id: "7",
        },
        {
          name: "Person1",
          id: "8",
        },
        {
          name: "Person1",
          id: "9",
        },
        {
          name: "Person1",
          id: "10",
        },
      ],
      isSubmit: false,
    };
  }, // console.log(1, element);

  methods: {
    handleDeleteLevel(id) {
      this.data = this.data.filter((item) => item.id !== id);
      this.data.map((item, index) => (item.level = index + 1));
      return this.data;
    },
    handleDeleConfirmPerson(id, level) {
      const levelEmployee = this.data.filter((item) => item.level == level);
      levelEmployee[0].employees?.filter((item) => item.id !== id);
      this.data.map((item) => {
        if (item.level == level) {
          item.employees = levelEmployee[0].employees?.filter(
            (item) => item.id !== id
          );
        }
      });
    },
    hanldeAddLevel() {
      if (this.data.length == 5) {
        this.errorMessage = "Had 5 level, Don't and level";
        setTimeout(() => (this.errorMessage = ""), 10000);
        return this.errorMessage;
      } else {
        this.errorMessage = "";
        const newLevel = { id: 121212, level: 1, employees: [] };
        this.data.unshift(newLevel);
        this.data.map((item, index) => {
          return (item.level = index + 1);
        });
        return this.data;
      }
    },
    handleSearch(searchName) {
      return this.data.user((item) => item.searchName == searchName);
    },
    handleClickSelectUser(id, level) {
      const newEmployee = this.user.filter((item) => item.id == id);
      this.data.map((item) => {
        if (item.level == level) {
          item.employees.push(newEmployee[0]);
        }
      });
      this.user = this.user.filter((item) => item.id != id);
      return this.data;
    },
    handleSubmit() {
      this.isSubmit = true;
      let flag = true;

      this.data.map((item) => {
        if (item.employees.length == 0) {
          flag = false;
          // console.log(item.level);
          document
            .getElementById(`${item.level}`)
            .scrollIntoView({ behavior: "smooth" });
          this.isSubmit = true;
          return flag;
        } else {
          flag = true;
        }
      });

      // document.getElementById("id").scrollIntoView({ behavior: "smooth" });
      // console.log(1, element);
      // element.scrollIntoView({ behavior: "smooth" });
      if (flag) {
        console.log(this.data);
      }
    },
  },
};
</script>

<style scoped>
.container {
  width: 924px;
  padding: 16px 32px;
  margin: 0 auto;

  border: 1px solid #dcdcdc;
  border-radius: 4px;
}
.title {
  margin-top: 16px;
  margin-bottom: 20px;
}
.plus__icon {
  width: 16px;
  height: 16px;
}
.btn__create {
  align-items: center;
  width: 136px;
  height: 32px;
  border: 1px solid #bcccdc;
  border-radius: 4px;
  background-color: #fff;
  margin-top: 22px;
  margin-bottom: 22px;
  cursor: pointer;
}
.error__message {
  color: red;
  font-size: 12px;
  font-weight: 300;
}
.level {
  width: 100%;
}
</style>
