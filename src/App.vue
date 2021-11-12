<template>
  <h1>Memory game</h1>
  <button @click="shuffleCards">New Game</button>
  <div class="card-grid">
    <SingleCard v-for="(card, index) in cards" 
      :key="index"
      :card="card"
      :match="card.matched"
      @choice="handleChoice"
      :flipped="card === choiceOne || card === choiceTwo || card.matched"
    />
  </div>
  <h3>Turns: {{ turns }}</h3>
</template>

<script>
import SingleCard from './components/SingleCard.vue'

const cardImages = [
  { src: 'https://i.ibb.co/QJTX1Wx/helmet-1.png', matched: false },
  { src: 'https://i.ibb.co/4MBJSvn/potion-1.png', matched: false },
  { src: 'https://i.ibb.co/4NPmCH2/ring-1.png', matched: false },
  { src: 'https://i.ibb.co/rGmqRJX/scroll-1.png', matched: false },
  { src: 'https://i.ibb.co/KXKJZLM/shield-1.png', matched: false },
  { src: 'https://i.ibb.co/zncNpcf/sword-1.png', matched: false },
]

export default {
  name: 'App',
  data(){
    return {
      cards: [],
      turns: 0,
      choiceOne: null,
      choiceTwo: null
    }
  },
  methods: {
    shuffleCards(){
      this.cards = [...cardImages, ...cardImages]
      .sort(() => Math.random() - 0.5)
      .map(card => ({ ...card, id: Math.random() }))

      this.turns = 0
    },
    handleChoice(card){
      this.choiceOne ? this.choiceTwo = card : this.choiceOne = card
      if (this.choiceOne && this.choiceTwo){
        if (this.choiceOne.src === this.choiceTwo.src) {
          this.cards = this.cards.map((card) => {
            if(card.src === this.choiceOne.src){
              return { ...card, matched: true }
            } else {
              return card
            }
          })
          console.log(this.cards);
          this.resetTurn()
        } else {
          setTimeout(() => this.resetTurn(), 1000)
        }
      }
    },
    resetTurn() {
      this.choiceOne = null
      this.choiceTwo = null
      this.turns = this.turns + 1
    }
  },
  mounted(){
    this.shuffleCards()
  },
  components: { SingleCard }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@100;200;300;400;500;600;700;800&display=swap');

/* base styles */
body {
  font-family: Raleway, sans-serif;
  margin: 0;
  font-size: 1.5em;
  text-align: center;
  background: #1b1523;
  color: #fff;
}
#app {
  max-width: 860px;
  margin: 40px auto;
}
button {
  background: none;
  border: 2px solid #fff;
  padding: 6px 12px;
  border-radius: 4px;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  font-size: 1em;
}
button:hover {
  background: #c23866;
  color: #fff;
}
.card-grid {
  margin-top: 40px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-gap: 20px;
}
</style>
