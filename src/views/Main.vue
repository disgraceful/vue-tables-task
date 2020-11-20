<template>
  <b-container fluid="sm">
    <b-card>
      <user-table :items="users"></user-table>
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
