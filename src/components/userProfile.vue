<template>
  <div class="user-profile">
    <div class="user-profile__panel">
      <h2 class="user-profile__username">@ {{ users.userName }}</h2>
      <div class="user-profile__admin" v-if="users.isAdmin">
        Admin
      </div>
      <div class="create-twoot-panel">
        <strong>followers </strong>{{ followers }}
        <button @click="followUser">Follow</button>
      </div>
      <!-- no need to pass params here from emmiting an event from child -->
      <CreateTwoot @add-twoot="addtwoot" />
    </div>
    <div class="user-profile__twoots-wrapper">
      <Twootitem
        v-for="twoot in users.twoots"
        :key="twoot.id"
        :twoot="twoot"
        :username="users.userName"
        @favourite="favouriteToggle"
      />
    </div>
  </div>
</template>

<script>
import Twootitem from "../components/Twootitem";
import CreateTwoot from "../components/CreateTwoot";

export default {
  name: "UserProfile",
  components: {
    Twootitem,
    CreateTwoot
  },
  data() {
    return {
      followers: 0,
      users: {
        id: 1,
        firstName: "Arham",
        lastName: "Chowdhury",
        userName: "_arhamchowdhury",
        email: "arhamchowdhry@gmail.com",
        isAdmin: true,
        twoots: [
          { id: 0, content: "Hi this is Arham Tweeting 1" },
          { id: 1, content: "Hi this is Arham Tweeting 2" }
        ]
      }
    };
  },
  watch: {
    followers(newFollowers, oldFollowers) {
      if (oldFollowers < newFollowers) {
        console.log(`you have gained a new ${this.users.userName}`);
      }
    }
  },
  computed: {
    fullName() {
      return `${this.users.firstName + this.users.lastName}`;
    }
  },
  methods: {
    followUser() {
      this.followers++;
    },
    favouriteToggle(id) {
      console.log(id);
    },

    addtwoot(e) {
      this.users.twoots.unshift({
        id: this.users.twoots.lenght,
        content: e
      });
    }
  },
  mounted() {
    this.followers++;
  }
};
</script>

<style scoped lang="scss">
.user-profile {
  display: flex;
  align-items: center;
}
.user-profile__panel {
  padding: 12px;
  background: #fff;
  flex-shrink: 1;
}
.user-profile__username {
  margin-bottom: 5px;
}
.user-profile__create-twoot {
  display: flex;
  flex-direction: column;
}
.user-profile__admin {
  padding: 6px;
  display: inline-block;
  background-color: darkslateblue;
  color: #fff;
  font-weight: 600;
  font-size: 13px;
  border-radius: 5px;
  margin-bottom: 12px;
}
.user-profile__twoots-wrapper {
  flex-shrink: 0;
  flex-grow: 1;
}
.create-twoot-panel {
  margin-top: 20px;
  padding: 20px 0;
  display: flex;
  flex-direction: column;
  textarea {
    border: 1px solid #dfe3e8;
    border-radius: 5px;
  }
  .create-twoot-panel__submit {
    display: flex;
    justify-content: space-between;
    .create-twoot-type {
      padding: 10px 0;
    }
    button {
      padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: deeppink;
      color: white;
      font-weight: bold;
    }
  }
  &.--exceeded {
    color: red;
    border-color: red;
    .create-twoot-panel__submit {
      button {
        background-color: red;
        color: white;
      }
    }
  }
}
</style>