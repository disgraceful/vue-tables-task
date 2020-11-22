<template>
  <b-container fluid="sm">
    <b-card>
      <user-table :items="users"></user-table>
      <hr />
      <b-row no-gutters>
        <b-col cols="auto" class="pr-2">
          <b-button>Add User</b-button>
        </b-col>
        <b-col cols="auto" class="px-2">
          <b-button>Clear All</b-button>
        </b-col>
      </b-row>
    </b-card>
  </b-container>
</template>

<script>
import UserTable from "@/components/Table.vue";
export default {
  components: {
    "user-table": UserTable,
  },

  data() {
    return {
      users: [
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
};
</script>

<style lang="scss" scoped></style>
