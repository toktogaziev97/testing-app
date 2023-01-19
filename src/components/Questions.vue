<template>
  <div><h2> Вопросы по тестированию экзамена </h2></div>
  <div v-if="question">
    <div v-for="(item, i) in question">
      <p>{{ item.id }}. {{ item.question }}</p>
      <div v-for="variant in item.variants" v-if="selected">
        <input type="radio" :name="item.id" :id="variant" :value="variant" v-model="selected[i].value">
        {{ variant }}
      </div>
      <p v-if="produce">{{result[i].checked ? 'правильно' : 'не правильно ' }}</p>
    </div>
    <button @click="submit">submit</button>
  </div>
</template>
<script>

export default {
  data: () => ({
    question: null,
    answer: null,
    produce: false,
    selected: null,
    result: null
  }),

  methods: {
    async getquestion() {
      const response = await fetch(`http://localhost:3000/questions`)
      const data = await response.json()
      this.question = await data
      this.selected = await data.map(item => ({
        value: null
      }))
    },

    async getanswer() {
      const response = await fetch(`http://localhost:3000/answers`)
      this.answer = await response.json()
    },

    submit() {
      this.result = this.answer.map ((item,i) =>  ({
        ...item,
        checked:this.selected[i].value === item.answer
      }))
      this.produce = true;
    }
  },

  mounted() {
    this.getquestion()
    this.getanswer()
  },
}
</script>