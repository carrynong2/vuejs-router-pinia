<script setup>
  import { ref,onMounted, watch } from 'vue';
  import { useRouter } from 'vue-router';
  import {useUserStore} from "../stores/user.js"

  const router = useRouter()
  const userStore = useUserStore()

  const isUpdated = ref(true)
  const firstname = ref("")
  const lastname = ref("")

  const backToHome = () => {
    router.push({name: "home"})
  }
  onMounted(() => {
    firstname.value = userStore.firstname;
    lastname.value = userStore.lastname;
  })
  watch([firstname, lastname], (newData) => {
    if (newData[0] !== userStore.firstname || newData[1] !== userStore.lastname) {
      isUpdated.value = false
    }
  })
  const updateProfile = () => {
    const formData = {
      firstname: firstname.value,
      lastname: lastname.value
    }
    userStore.changeName(formData)
    isUpdated.value = true
  }
</script>

<template>
  <div>
    Profile from stores
    <div v-if="isUpdated" style="color: blue;">
      Profile up to date
    </div>
    <div>Firstname {{ userStore.firstname }}</div>
    <div>Lastname {{ userStore.lastname }}</div>
    <div>Fullname: {{ userStore.fullname }}</div>
  </div>
  <div>
    Profile Vue
    <div>
      Firstname <input type="text" v-model="firstname">
    </div>
    <div>
      Lastname <input type="text" v-model="lastname">
    </div>
    <button @click="updateProfile()">Update Profile</button>
    <div>
        <button @click="backToHome()">Back to home</button>
    </div>
  </div>
</template>