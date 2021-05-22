<template>
  <div class="background">
    <div>
      <h1 class="titulo">{{ info.title }}</h1>
      <p class="year">{{ info.year }}</p>
      <img class="img" v-bind:src="info.img" v-bind:alt="info.alt" />
      <div>
        <star-rating v-model="rating"></star-rating>
      </div>
      <button class="rate" @click="rate">Calificar</button>
    </div>
  </div>
</template>

<script>
import StarRating from "vue-star-rating";
import axios from "axios";
export default {
  components: {
    StarRating,
  },
  name: "Cartoon",
  props: {
    msg: String,
  },
  data() {
    return {
      info: [],
      rating: 0,
    };
  },

  mounted() {
    console.log("entrando");
    this.getCartoon();
  },

  methods: {
    getRamdom(min = 1, max = 2466) {
      return parseInt(Math.random() * (max - min) + min);
    },
    getCartoon() {
      let number = this.getRamdom();
      let url = "https://xkcd.com/" + number + "/info.0.json";
      axios.get(url).then((response) => {
        console.log(response);
        this.info = response.data;
      });
    },
    rate() {
      if (this.rating != 0) {
        this.$toast.open(
          "has calificado: " + this.rating + " Gracias por tu Calificación "
        );
        this.getCartoon();
        this.rating = 0;
      } else {
        this.$toast.open({
          message: "Elija una Calificación correcta",
          type: "error",
        });
      }
    },
  },
};
</script>

<style scoped>
.background {
  background-color: #767b7f;
}
.titulo {
  font-style: bold;
  color: white;
  font-weight: 900;
}
.img {
  margin-bottom: 8px;
}
.vue-star-rating {
  width: 14%;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 30px;
  margin-top: 21px;
  
}

.rate {
        font-size: 23px;
    background: white;
    border-radius: 9px;
    width: 131px;
    font-weight: 200;
    cursor: pointer;
}

.year{
    color: white;
    font-weight: 400;

}
</style>