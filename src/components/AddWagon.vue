<template>
  <div class="flex justify-start space-x-4 place-items-center">
    <label for="wagon">Wpisz numer wagonu</label>
    <input
      @change="wrongNumber = false"
      @keyup.enter="addWagon"
      class="text-black h-12 text-lg placeholder-gray-400"
      type="number"
      id="wagon"
      ref="wagonInput"
      maxlength="12"
      placeholder="nr wagonu"
    />
    <button @click="addWagon">Dodaj</button>
    <span class="text-red-400" v-show="wrongNumber"
      >Wpisałeś za krótki nr wagonu lub próbujesz dodać ponownie ten sam
      wagon</span
    >
  </div>
  <div>
    <ul class="flex flex-col w-1/3 my-8">
      <li
        class="flex justify-around border-gray-400 border-2"
        v-for="(wagon, index) in wagons"
        :key="index"
      >
        <span>Nr:{{ index + 1 }}</span>

        {{ wagon.wagon }}
        <button class="text-red-400" @click="deleteWagon(index)">Usuń</button>
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
        this.wagons.some(({ wagon }) => (wagon === wagonNumber ? true : false))
      ) {
        this.wrongNumber = true;
        return;
      } else {
        this.wagons.push({ wagon: wagonNumber });
        this.$refs.wagonInput.value = "";
      }
    },
    deleteWagon(id) {
      this.wagons.splice(id, 1);
    },
  },
};
</script>

<style scoped></style>
