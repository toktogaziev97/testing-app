<template>
<div v-for="item in INFORMATION">
  <p class="questions">{{ item.question }}</p>
  {{ item.variants }}
</div>
</template>
<script>
export default {
  data: () => ({
    INFORMATION: null
  }),
  methods: {
    async getdata() {
      const response = await fetch(`http://localhost:3000/questions`)
      this.INFORMATION = await response.json()
    }
  },
  mounted() {
    this.getdata()
  }
}
</script>
