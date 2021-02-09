<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
  <div>
    <label for="wagon">Wpisz numer wagonu</label>
    <span class="text-red-400" v-if="wrongNumber"
      >Wpisałeś za krótki nr wagonu lub próbujesz dodać ponownie ten sam
      wagon</span
    >
    <input
      @change="wrongNumber = false"
      @keyup.enter="addWagon"
      class="text-black"
      type="number"
      id="wagon"
      ref="wagonInput"
    />
    <button @click="addWagon">Dodaj</button>
  </div>
  <div>
    <ul>
      <li v-for="(wagon, index) in wagons" :key="index">
        {{ wagon.wagonNumber }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "AddWagon",
  props: {
    msg: String,
  },
  data() {
    return {
      wagons: [],
      wrongNumber: false,
    };
  },
  methods: {
    addWagon() {
      const wagonNumber = this.$refs.wagonInput.value;
      const wagonNormalLength = 12;

      if (
        wagonNumber.length !== wagonNormalLength ||
        this.wagons.includes(wagonNumber)
      ) {
        this.wrongNumber = true;
        return;
      } else {
        this.wagons.push({ wagonNumber });
        this.$refs.wagonInput.value = "";
        console.log(this.wagons);
      }
    },
  },
};
</script>

<style scoped></style>
