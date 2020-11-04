<template>
  <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot">
    <label for="newTwoot">
      <strong>New Twoot</strong>
    </label>
    <div>({{ newTwootCharCout }}/180)</div>
    <textarea id="newTwoot" rows="4" v-model="state.newTwootContent"></textarea>

    <div class="user-profile__select">
      <select v-model="state.selectedTwootType">
        <option
          :value="option.value"
          v-for="(option, index) in state.twootsTypes"
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
import { reactive, computed } from "vue";
export default {
  name: "Createtwoot",

  //setup has two params by default the first params is props
  //the second params is used to for emitting the emit event of specific component
  setup(props, context) {
    const state = reactive({
      newTwootContent: "",
      textCharcount: "",
      selectedTwootType: "instant",
      twootsTypes: [
        { value: "draft", name: "Draft Twoot" },
        { value: "instant", name: "Instant Twoot" }
      ]
    });
    const newTwootCharCout = computed(() => state.newTwootContent.length);
    function createNewTwoot() {
      if (state.newTwootContent != "" && state.selectedTwootType != "draft") {
        console.log(state.newTwootContent + state.selectedTwootType);
        context.emit("add-twoot", state.newTwootContent);
        state.newTwootContent = "";
      }
    }

    return {
      state,
      newTwootCharCout,
      createNewTwoot
    };
  }
};
</script>

<style scoped>
</style>