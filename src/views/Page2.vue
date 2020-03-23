<template>
  <div class="page2">
    <table class="persons">
      <tr>
        <th>name</th>
        <th>surname</th>
        <th>phone</th>
        <th>email</th>
      </tr>
      <tr v-for="(person) in persons" :key="person" class="person">
          <td><input type="text" v-model="person.name"  @change="changePerson"></td>
          <td><input type="text" v-model="person.surname" @change="changePerson"></td>
          <td><input type="tel" v-model="person.phone" @change="changePerson"></td>
          <td><input type="email" v-model="person.email" @change="changePerson"></td>
      </tr>
    </table>
    <br>
    <input type="text" :placeholder="'Import JSON'" v-model="newPerson" @change="addPerson" />
    <button @click="addOnePerson">Add user</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      persons: [
        {
          name: "Bob",
          surname: "Marli",
          phone: 38062034984,
          email: "bob@gmail.com"
        },
        {
          name: "Sem",
          surname: "Vinchester",
          phone: 380620477576,
          email: "sem@gmail.com"
        },
        {
          name: "Din",
          surname: "Vinchester",
          phone: 380628597883,
          email: "din@gmail.com"
        }
      ],
      newPerson: null
    };
  },
  mounted() {
    if (localStorage.getItem("persons")) {
      try {
        this.persons = JSON.parse(localStorage.getItem("persons"));
      } catch (e) {
        localStorage.removeItem("persons");
      }
    }
  },
  watch: {},
  methods: {
    addOnePerson() {
      this.newPerson = {};
      this.addPerson();
    },
    addPerson() {
      if (Object.keys(this.newPerson).length !== 0) { 
        this.newPerson = JSON.parse(this.newPerson);
      }
      Array.isArray(this.newPerson) ? this.persons.push(...this.newPerson) : this.persons.push(this.newPerson);
      this.savePersons();
      this.newPerson = null;
    },
    changePerson() {
      this.savePersons();
    },
    savePersons() {
      const parsed = JSON.stringify(this.persons);
      localStorage.setItem("persons", parsed);
    }
  }
};
</script>

<style lang="less" scoped>
.persons {
  input {
    border: none;
    outline: none;
    text-align: center;
    width: 100%;
  }
}
</style>
