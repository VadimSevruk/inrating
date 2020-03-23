<template>
  <div class="home">
    <table class="persons">
      <tr>
        <th>name</th>
        <th>surname</th>
        <th>phone</th>
        <th>email</th>
      </tr>
      <tr v-for="(person, n) in persons" :key="person.name" class="person">
        <td>{{person.name}}</td>
        <td>{{person.surname}}</td>
        <td>{{person.phone}}</td>
        <td>{{person.email}}</td>
        <td><button @click="removePerson(n)">delete</button></td>
        <td><router-link to="/page2">edit</router-link></td>
    </tr>
    </table>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  data() {
    return {
      persons: []
    }
  },
  mounted() {
    if (localStorage.getItem("persons")) {
      try {
        this.persons = JSON.parse(localStorage.getItem("persons"));
      } catch(e) {
        localStorage.removeItem("persons");
      }
    }
  },
  methods: {
    removePerson(x) {
      this.persons.splice(x, 1);
      this.savePersons();
    },
    savePersons() {
      const parsed = JSON.stringify(this.persons);
      localStorage.setItem("persons", parsed);
    }
  }
};
</script>

<style lang="less">
.persons {
  width: 60%;
  margin: 0 auto;
  border-collapse: collapse;

  td,
  th {
    width: 25%;
    border: 1px solid black;
  }

  button {
    width: 100%;
    border: none;
    cursor: pointer;
  }

  a {
    text-decoration: none;
    color: #000;
    background-color: #f0f0f0;
    cursor: pointer;
    padding: 1px 6px;
    font-size: 13px;
  }
}
</style>
