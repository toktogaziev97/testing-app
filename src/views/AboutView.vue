<template>
  <div class="base">
    <div class="base_col">
      <Questions/>
    </div>
  </div>
</template>
<script>

import questions from '../components/Questions.vue';
export default {
  components:{
    'Questions':questions,
  }
}
</script>