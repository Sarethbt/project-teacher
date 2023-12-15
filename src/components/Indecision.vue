<template>
  <img v-if="img" :src="img" alt="bg" />
  <div class="bg-dark"></div>

  <div class="indecision-container">
    <input type="text" placeholder="Hazme una pregunta" v-model="question" />
    <p>Recuerda terminar con un signo de interrogación (?)</p>

    <div v-if="isValidQuetion">
      <h2>{{ question }}</h2>
      <h1>{{answer}}</h1>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      question: null,
      answer: null,
      img: null,
      isValidQuetion: false 
    }
  },

  methods: {
    async getAsnwer (){
     this.answer = 'Pensando...'

     const {answer, image} = await fetch ('https://yesno.wtf/api').then(r => r.json())

     this.answer = answer === 'yes' ? 'Sí!' : 'No!'
     this.img = image
    }
  },

  watch: {
    question(Value) {
      this.isValidQuetion= false 
      if(!Value.includes("?")) return
      this.isValidQuetion = true 
      this.getAsnwer ()
    },
  },
}
</script>

<style scoped>
img,
.bg-dark {
  height: 100vh;
  left: 0;
  object-fit: cover;
  position: fixed;
  top: 0;
  width: 100vw;
}

.bg-dark {
  background-color: rgba(0, 0, 0, 0.4);
}

.indecision-container {
  text-align: center;
  position: relative;
  z-index: 99;
}

input {
  width: 250px;
  padding: 10px 15px;
  border-radius: 5px;
  border: none;
}
input:focus {
  outline: none;
}

p {
  color: white;
  font-size: 20px;
  margin-top: 0px;
}

h1,
h2 {
  color: white;
}

h2 {
  margin-top: 150px;
}
</style>
