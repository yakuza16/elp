<template>
  <div class="flex justify-start space-x-4 place-items-center">
    <div class="border-2 flex space-x-6">
      <label for="type">Typ wagonu:</label>
      <select ref="type" id="type" class="text-black">
        <option value="kgns">Kgns</option>
        <option value="sgs" selected>Sgs</option>
        <option value="sggrss">Sggrss</option>
        <option value="rgmms">Rgmms</option>
        <option value="sdgmnss">Sdgmnss</option>
      </select>
    </div>
    <div class="border-2 flex place-items-center space-x-6">
      <label for="wagon">Wpisz numer wagonu</label>
      <input
        @input="wrongNumber = false"
        @keyup.enter="addWagon"
        class="text-black h-12 text-lg placeholder-gray-400"
        maxlength="12"
        id="wagon"
        ref="wagonInput"
        placeholder="nr wagonu"
      />
    </div>
    <button class="rounded-lg border-2 px-4" @click="addWagon">Dodaj</button>
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
        <span>Typ: {{ wagon.wagonType }}</span>

        {{ wagon.wagonNumber }}
        <button
          class="rounded-lg border-2 px-4 text-red-400"
          @click="deleteWagon(index)"
        >
          Usuń
        </button>
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
      const wagonType = this.$refs.type.value;
      const wagonNormalLength = 12;

      if (
        wagonNumber.length !== wagonNormalLength ||
        this.wagons.some(({ wagon }) => (wagon === wagonNumber ? true : false))
      ) {
        this.wrongNumber = true;
        console.log(this.$refs.type.value);
        return;
      } else {
        this.wagons.push({ wagonNumber, wagonType });
        this.$refs.wagonInput.value = "";
        console.log(this.wagons);
      }
    },
    deleteWagon(id) {
      this.wagons.splice(id, 1);
    },
  },
};
</script>

<style scoped></style>
