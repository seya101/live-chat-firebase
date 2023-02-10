<template>
  <div class="chatroom-content">
    <div class="container">
    <Navbar />
    <ChatWindows/>
    <NewChatForm/>
  </div>
  </div>
  
</template>

<script>
import Navbar from "../components/Navbar.vue";
import getUser from "../composables/getUser";
import { watch } from "vue";
import { useRouter } from "vue-router";
import NewChatForm from "../components/NewChatForm.vue";
import ChatWindows from "../components/ChatWindows.vue";

export default {
  components: { Navbar, NewChatForm, ChatWindows },
  setup() {
    const router = useRouter();
    const { user } = getUser();

    // if the user value is ever null, redirect to welcome screen
    watch(user, () => {
      if (!user.value) {
        router.push({ name: "Welcome" });
      }
    });
  },
};
</script>

<style scope>
.chatroom-content {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
