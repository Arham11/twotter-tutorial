<template>
  <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot">
    <label for="newTwoot">
      <strong>New Twoot</strong>
    </label>
    <div>hi {{ textCharcount }}</div>
    <textarea
      id="newTwoot"
      rows="4"
      v-model="newTwootContent"
      @keyup="textCount"
    ></textarea>

    <div class="user-profile__select">
      <select v-model="selectedTwootType">
        <option
          :value="option.value"
          v-for="(option, index) in twootsTypes"
          :key="index"
        >
          {{ option.name }}
        </option>
      </select>
    </div>

    <button>Twoot!</button>
  </form>
</template>

<script lang="ts">
export default {
  name: "Createtwoot",
  data() {
    return {
      newTwootContent: "",
      textCharcount: "",
      selectedTwootType: "instant",
      twootsTypes: [
        { value: "draft", name: "Draft Twoot" },
        { value: "instant", name: "Instant Twoot" }
      ]
    };
  },
  methods: {
    createNewTwoot() {
      if (this.newTwootContent != "" && this.selectedTwootType != "draft") {
        console.log(this.newTwootContent + this.selectedTwootType);

        this.$emit("add-twoot", this.newTwootContent);

        // this.users.twoots.unshift({
        //   id: this.users.lenght,
        //   content: this.newTwootContent
        // });
        this.newTwootContent = "";
      }
    },
    textCount() {
      return (this.textCharcount = this.newTwootContent.lenght);
    }
  }
};
</script>

<style scoped>
</style>