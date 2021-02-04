<template>
  <div class="home">
    <p class="description">Press the numbers from 0 to 9 to discover them</p>
    <ul>
      <li
        v-for="(num, i) in numbers"
        :key="i"
        :class="[{ active: active(`${num.number}`) }]"
      >
        <span>{{ num.number }}</span>
        <div v-if="num.number !== 0" class="animals">
          <img
            v-for="no in num.number"
            :src="require(`@/assets/${num.img}.png`)"
            :alt="num.img"
            :key="no"
          />
        </div>
      </li>
    </ul>

    <button
      class="reset-button"
      @click="
        findedNumbers = [];
        number = null;
      "
      style=""
    >
      Reset
    </button>
  </div>
</template>

<script>
export default {
  name: "Home",
  data: () => ({
    number: null,
    findedNumbers: [],
    numbers: [
      { number: 7, color: "gold", img: "aries" },
      { number: 8, color: "brown", img: "butterfly" },
      { number: 9, color: "green", img: "lion" },
      { number: 4, color: "pink", img: "dog" },
      { number: 5, color: "orange", img: "cat" },
      { number: 6, color: "lime", img: "chicken" },
      { number: 1, color: "yellow", img: "sheep" },
      { number: 2, color: "blue", img: "cow" },
      { number: 3, color: "purple", img: "pig" },
      { number: 0, color: "red", img: "" }
    ]
  }),
  methods: {
    _keyListener(e) {
      this.number = e.key;

      if (
        ((e.keyCode >= 48 && e.keyCode <= 57) ||
          (e.keyCode >= 96 && e.keyCode <= 105)) &&
        !this.findedNumbers.find(num => num === e.key)
      ) {
        this.findedNumbers.push(e.key);
      }
    },
    active(number) {
      return this.findedNumbers.find(num => num === number);
    }
  },
  mounted() {
    window.addEventListener("keypress", this._keyListener);
  },
  beforeDestroy() {
    window.removeEventListener("keypress", this._keyListener);
  }
};
</script>

<style lang="scss">
body {
  background-color: #34e4ea;
}
</style>

<style lang="scss" scoped>
.description {
  font-size: 38px;
}

ul {
  display: flex;
  list-style: none;
  flex-wrap: wrap;
  max-width: 1320px;
  padding: 40px 0;
  margin: 0 auto;

  & > li {
    max-height: 200px;
    text-align: center;
    border: 2px solid black;
    margin: 5px;
    flex: 1 0 24%;
    font-size: 200px;
    display: flex;
    justify-content: center;
    padding: 10px;

    border-color: black;
    border-style: dashed;

    span {
      opacity: 0;
    }

    .animals {
      opacity: 0;
      display: flex;
      max-width: 220px;
      flex: 1 0 50%;
      flex-wrap: wrap;
      align-items: center;
      justify-content: center;
    }

    &.active {
      span,
      .animals {
        opacity: 1;
      }
    }
  }
}

.reset-button {
  font-size: 40px;
  padding: 15px 25px;
}
</style>
