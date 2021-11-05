<template>
  <div>
    <h1>Tasks</h1>
    <input type="text" v-model="userInput" />
    <button @click="addUser">Add user</button>
    <p>{{ userInput }}</p>
    <div v-for="user in users" :key="users.indexOf[user]">
      <ul>
        <input
          type="text"
          v-model="user.name"
          :disabled="!isEditing"
          :class="{ view: !isEditing }"
        />
        <button @click="isEditing = !isEditing" v-if="!isEditing">Edit</button>
        <button @click="save" v-else-if="isEditing">Save</button>
        <button v-if="isEditing" @click="cancel">Cancel</button>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Tasks",
  data() {
    return {
      isEditing: false,
      userInput: "",
      users: [{ name: "sirius" }, { name: "michelle" }],
    };
  },
  methods: {
    addUser() {
      console.log(this.userInput);
      this.users.push({ name: this.userInput });
    },

    save() {
      this.cachedUser = Object.assign({}, this.users);
      this.isEditing = false;
    },
    cancel() {
      this.users = Object.assign({}, this.cachedUser);
      this.isEditing = false;
    },
  },
  mounted() {
    this.cachedUser = Object.assign({}, this.users);
  },
};
</script>

<style></style>
