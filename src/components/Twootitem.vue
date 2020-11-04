<template>
  <div class="twoot-item" @click="favouriteTwoot(twoot.id)">
    <div>@ {{ username }}</div>
    <div>{{ twoot.content }}</div>
  </div>
</template>

<script lang="ts">
export default {
  name: "Twooittem",
  props: {
    username: {
      type: String,
      required: true
    },
    twoot: {
      type: String,
      required: true
    }
  },
  setup(props, context) {
    function favouriteTwoot(id) {
      context.emit("favourite", id);
    }

    return {
      favouriteTwoot
    };
  }
};
</script>

<style scoped>
.twoot-item {
  padding: 15px;
  background-color: #fff;
  margin: 20px;
  transition: all 0.25s ease;
  cursor: pointer;
}
.twoot-item:hover {
  transform: scale(1.05, 1.05);
}
</style>