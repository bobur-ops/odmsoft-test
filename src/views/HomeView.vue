<script>
import UsersTable from "@/components/UsersTable.vue";
import { dummyUsers } from "../constants/dummyData";

export default {
  components: {
    UsersTable,
  },
  data() {
    return {
      users: [],
      limit: 100,
      isSortByName: true,
      searchQuery: "",
      selectOptions: [
        {
          value: "first_name",
          text: "Name",
          id: 1,
        },
        {
          value: "last_name",
          text: "Last Name",
          id: 2,
        },
        {
          value: "email",
          text: "Email",
          id: 3,
        },
        {
          value: "ip_address",
          text: "IP address",
          id: 4,
        },
        {
          value: "gender",
          text: "Gender",
          id: 5,
        },
      ],
      activeSearchItem: "first_name",
    };
  },
  mounted() {
    this.users = this.sortUsers("first_name");
    this.getMoreUsers();
  },
  methods: {
    sortUsers(sortType) {
      let res = [];
      if (this.searchQuery) {
        const data = dummyUsers.filter((item) =>
          item[this.activeSearchItem]
            .toLowerCase()
            .includes(this.searchQuery.toLowerCase())
        );
        res = data.sort((a, b) => a[sortType].localeCompare(b[sortType]));
      } else {
        res = dummyUsers.sort((a, b) => a[sortType].localeCompare(b[sortType]));
      }

      return res;
    },
    sort(sortType) {
      this.users = this.sortUsers(sortType);
      if (sortType === "gender") {
        this.isSortByName = false;
      } else {
        this.isSortByName = true;
      }
    },
    getMoreUsers() {
      window.onscroll = () => {
        let bottomOfWindow =
          document.documentElement.scrollTop + window.innerHeight ===
          document.documentElement.offsetHeight;
        if (bottomOfWindow) {
          this.limit += 50;
        }
      };
    },
    handleSwitchSelect(value) {
      this.activeSearchItem = value;
      this.searchUsers();
    },
    searchUsers() {
      const newUsers = dummyUsers.filter((item) =>
        item[this.activeSearchItem]
          .toLowerCase()
          .includes(this.searchQuery.toLowerCase())
      );
      this.users = [...newUsers];
    },
  },
};
</script>

<template>
  <div class="wrapper">
    <div class="search-bar">
      <div class="custom-select">
        <select @change="(e) => handleSwitchSelect(e.target.value)">
          <option
            v-for="item in selectOptions"
            :key="item.id"
            :value="item.value"
          >
            {{ item.text }}
          </option>
        </select>
      </div>
      <input v-model="searchQuery" type="text" placeholder="search..." />
      <button @click="searchUsers">Search</button>
    </div>
    <div class="sort-status">
      Sorting by <span> {{ isSortByName ? "Name" : "Gender" }}</span> (click on
      <span>name</span> or <span>gender</span> at the top of table to switch)
    </div>
    <users-table @sort="sort" :users="users.slice(0, limit)" />
  </div>
</template>
<style scoped>
.wrapper {
  max-width: 1174px;
  margin: 0 auto;
  padding-top: 20px;
}
.sort-status {
  margin-bottom: 15px;
  padding-left: 10px;
  margin-top: 15px;
}
.sort-status span {
  color: blue;
}
.search-bar {
  width: 70%;
  margin: 0 auto;
  display: flex;
  gap: 10px;
}
.search-bar input {
  flex: 1;
  outline: none;
  border: 1px solid #e2e8f0;
  border-radius: 6px;
  padding-left: 10px;
}
.search-bar button {
  padding: 10px;
  background: #e2e8f0;
  cursor: pointer;
  border: none;
  outline: none;
  border-radius: 6px;
  font-size: 17px;
}
select {
  height: 100%;
  border: 1px solid #e2e8f0;
  outline: none;
  border-radius: 6px;
  padding: 0 10px;
}
select option {
  padding: 10px;
}
</style>
