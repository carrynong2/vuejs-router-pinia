<script setup>
  import { RouterLink,useRoute,useRouter } from 'vue-router';
  const route = useRoute()
  const router = useRouter()
  const backToHome = () => {
    router.push({name: "home"})
  }
</script>

<template>
  <div>
    Profile Vue
    <div>
      Firstname <input type="text">
    </div>
    <div>
      Lastname <input type="text">
    </div>
    <div>
        <button @click="backToHome()">Back to home</button>
    </div>
  </div>
</template>