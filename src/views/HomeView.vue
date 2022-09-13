<template>
  <div class="home container">
    <div>
      <table class="table py-5 my-5">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">User Name</th>
            <th scope="col">Roles</th>
            <th scope="col">Submit</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="i in users.data.data">
            <th scope="row">{{ i.id }}</th>
            <td>{{ i.name }}</td>
            <td>
              <input type="checkbox" id="first" name="name1" value="Admin">
              <label for="first">Admin</label><br/>
              <input type="checkbox" id="second" name="name1" value="Superadmin">
              <label for="second">Superadmin</label><br/>
              <input type="checkbox" id="third" name="name1" value="Moderator">
              <label for="third">Moderator</label><br/>
              <input type="checkbox" id="fourth" name="name1" value="Basic">
              <label for="fourth">Basic</label>
            </td>
            <td>
              <button class="btn btn-primary">Submit</button></td>
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
  components: {
  },
  data() {
    return {
      users: null,
    }
  },
  mounted () {
    axios.get('http://127.0.0.1:8000/api/users').then(response => (this.users = response))
  }
}
</script>
