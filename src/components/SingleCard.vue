<template>
  <div class="card" @click="handleClick">
      <div :class="{'flipped': flipped}">
        <img class="front" :src="card.src" alt="card front" />
        <img class="back" src="https://i.ibb.co/YQyT987/cover.png"  alt="cover" />
      </div>
    </div>
</template>


<script>
export default {
    props: ["card", 'matched', "flipped"],
    methods: {
        handleClick(){
            this.$emit('choice', this.card)
        }
    }
}
</script>

<style>
.card {
  position: relative;
}
.card img {
  width: 100%;
  display: block;
  border: 2px solid #fff;
  border-radius: 6px;
}

/* front of card - the picture */
.card .front {
  transform: rotateY(90deg);
  transition: all ease-in 0.2s;
  position: absolute;
}
.flipped .front {
  transform: rotateY(0deg);
  transition-delay: 0.2s;
}

/* back of card - cover */
.card .back {
  transition: all ease-in 0.2s;
  transition-delay: 0.2s;
}
.flipped .back {
  transform: rotateY(90deg);
  transition-delay: 0s;
}
</style>