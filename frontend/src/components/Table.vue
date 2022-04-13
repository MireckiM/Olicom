<template>
  <v-container>
    <v-row>
      <v-col></v-col>
      <v-col xl="6" lg="6" md="6" sm="12" xs="12">
        <div v-for="user in this.users" v-bind:key="user.id">
          <v-card class="green lighten-1 mb-3">
            name: {{ user.name }} email: {{ user.email }} company:
            {{ user.company.name }} adress: {{ user.address.city }} website:
            {{ user.website }}
          </v-card>
        </div>
      </v-col>
      <v-col></v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Table",
  data() {
    return {
      users: {},
      page: 1,
    };
  },
  methods: {
    getUsers() {
      fetch("https://jsonplaceholder.typicode.com/users")
        .then((response) => response.json())
        .then((json_data) => (this.users = json_data));
      console.log("ok");
    },
  },

  created() {
    this.getUsers();
  },
};
</script>