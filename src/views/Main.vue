<template>
  <b-container fluid="sm">
    <b-card>
      <b-card-title> Users</b-card-title>
      <b-card-text v-if="users.length < 1">No users found</b-card-text>
      <user-table
        :items="users"
        :addFnc="spliceUser"
        :editFnc="editUser"
        :deleteFnc="deleteUser"
      ></user-table>
      <hr />
      <b-row no-gutters>
        <b-col cols="auto" class="mr-2">
          <b-button v-b-modal.global-modal>Add User</b-button>
        </b-col>
        <b-col cols="auto" class="mx-2">
          <b-button v-b-modal.global-confirm>Clear All</b-button>
        </b-col>
      </b-row>
    </b-card>
    <record-modal id="global-modal" :okFnc="addUser"></record-modal>
    <confirm-modal id="global-confirm" :okFnc="clearUsers">
      Are you sure you want to delete all users?
    </confirm-modal>
  </b-container>
</template>

<script>
import UserTable from "@/components/Table.vue";
import Modal from "@/components/Modal.vue";
import ConfirmModal from "@/components/ConfirmModal.vue";
export default {
  components: {
    "user-table": UserTable,
    "record-modal": Modal,
    "confirm-modal": ConfirmModal,
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
        this.saveUsers();
      }
    },

    deleteUser(index) {
      if (this.users[index]) {
        this.users.splice(index, 1);
        this.saveUsers();
      }
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
