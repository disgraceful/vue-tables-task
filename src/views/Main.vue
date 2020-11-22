<template>
  <b-container fluid="sm">
    <b-card>
      <user-table
        :items="users"
        :addFnc="spliceUser"
        :editFnc="editUser"
        :deleteFnc="deleteUser"
      ></user-table>
      <hr />
      <b-row no-gutters>
        <b-col v-b-modal.global-modal cols="auto" class="mr-2">
          <b-button>Add User</b-button>
        </b-col>
        <b-col cols="auto" class="mx-2">
          <b-button>Clear All</b-button>
        </b-col>
      </b-row>
    </b-card>
    <record-modal id="global-modal" :okFnc="addUser"></record-modal>
  </b-container>
</template>

<script>
import UserTable from "@/components/Table.vue";
import Modal from "@/components/Modal.vue";
export default {
  components: {
    "user-table": UserTable,
    "record-modal": Modal,
  },

  data() {
    return {
      users: [],
      defaultUsers: [
        {
          name: "Brad",
          surname: "Gibson",
          email: "brad.gibson@gmail.com",
        },
        {
          name: "John",
          surname: "Smith",
          email: "john.smith@gmail.com",
        },
        {
          name: "Jane",
          surname: "Smith",
          email: "jane.smith@gmail.com",
        },
      ],
    };
  },
  methods: {
    addUser(user) {
      this.users.push(user);
      this.saveUsers();
    },

    spliceUser(index, user) {
      this.users.splice(index, 0, user);
      this.saveUsers();
    },

    editUser(index, user) {
      if (this.users[index]) {
        this.users.splice(index, 1, user);
      }
      this.saveUsers();
    },

    deleteUser(user) {
      this.users = this.users.filter((u) => user.email !== u.email);
      this.saveUsers();
    },

    saveUsers() {
      localStorage.setItem("users", JSON.stringify(this.users));
    },

    retrieveUsers() {
      const storedUsers = localStorage.getItem("users");
      if (storedUsers) {
        this.users = JSON.parse(storedUsers);
      } else {
        this.users = this.defaultUsers;
      }
    },

    clearUsers() {
      this.users = [];
      this.saveUsers();
    },
  },
  created() {
    this.retrieveUsers();
  },
};
</script>

<style lang="scss" scoped></style>
