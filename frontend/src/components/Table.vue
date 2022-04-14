<template>
  <v-container>
    <v-row><v-col></v-col></v-row>
    <v-row>
      <v-col></v-col>
      <v-col xl="10" lg="10" md="10" sm="12" xs="12">
        <!--{{ this.users }}-->
        <div v-for="user in this.users" v-bind:key="user.id"></div>
        <v-card class="light green lighten-4">
          <v-card-title>
            Users
            <v-spacer></v-spacer>
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
          </v-card-title>
          <v-data-table
            class="light green lighten-4"
            :headers="headers"
            :items="users"
            :search="search"
            :footer-props="{
              'items-per-page-options': [3, 10],
            }"
            :items-per-page="10"
          >
            <template #item.email="{ item }">
              <a target="_blank" :href="`mailto:${item.email}`">
                {{ item.email }}
              </a>
            </template>
          </v-data-table>
        </v-card>
      </v-col>
      <v-col></v-col>
    </v-row>
    <v-row><v-col></v-col></v-row>
  </v-container>
</template>

<script>
export default {
  name: "Table",
  data() {
    return {
      users: [],
      search: "",
      headers: [
        {
          text: "Name",
          align: "start",
          value: "name",
        },
        { text: "Email", value: "email" },
        { text: "Company", value: "company.name" },
        { text: "Adress", value: "address.city" },
        { text: "Website", value: "website" },
      ],
    };
  },
  methods: {
    getUsers() {
      fetch("https://jsonplaceholder.typicode.com/users")
        .then((response) => response.json())
        .then((json_data) => (this.users = json_data));
    },
  },

  created() {
    this.getUsers();
  },
};
</script>