<template>
  <div class="home container">
    <div>
      <table class="table py-5 my-5">
        <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">User Name</th>
          <th scope="col">Roles</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="i in users.data.data">
          <th scope="row">{{ i.id }}</th>
          <td>{{ i.name }}</td>
          <td>
            <div v-for="item in roles.data.data">
              <input type="checkbox" :id="item.id" :name="item.name"
                     :value="item.name"
                     :checked="roleIndexes(i.roles).indexOf(item.id) !== -1"
                     @click="save(i.id, item.id)">
              <label :for="item.id">
                {{ item.name }}
              </label>
            </div>
          </td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

import axios from "axios";

export default {
  name: 'HomeView',
  components: {},
  data() {
    return {
      users: null,
      roles: null,
    }
  },
  mounted() {
    axios.get('http://127.0.0.1:8000/api/users').then(response => (this.users = response));
    axios.get('http://127.0.0.1:8000/api/roles').then(response => (this.roles = response));
  },
  methods: {
    save(a, b) {
      axios.post('http://127.0.0.1:8000/api/users/'+a+'/'+b).then(function (response) {
        console.log(response)
      });
    },
  },
  computed: {
    roleIndexes() {
      return (arr) => arr.map(a => a.id)
    }
  }
}
</script>
