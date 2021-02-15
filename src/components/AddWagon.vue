<template>
  <div class="flex justify-start space-x-4 place-items-center text-xs">
    <div class="border-2 flex space-x-6">
      <label for="type">Typ wagonu:</label>
      <select ref="type" id="type" class="text-black">
        <option value="kgns">Kgns</option>
        <option value="sgs" selected>Sgs</option>
        <option value="sggrss">Sggrss</option>
        <option value="rgmms">Rgmms</option>
        <option value="sdgmnss">Sdgmnss</option>
        <option value="sgns">Sgns</option>
        <option value="sggrs">Sggrs</option>
        <option value="sggmrss">Sggmrss</option>
      </select>
    </div>
    <div class="border-2 flex place-items-center space-x-6">
      <label for="wagon">Wpisz numer wagonu</label>
      <input
        @input="checkLength"
        @keyup.enter="addWagon"
        class="text-black h-12 text-xs placeholder-gray-400"
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
  <div class="text-xs">
    <ul class="flex flex-col my-8">
      <li
        class="flex justify-start place-items-center space-x-4  border-gray-400 border-2"
        v-for="({ wagonNumber, wagonType, axis, wagonTare, maxPayload },
        index) in wagons"
        :key="index"
      >
        <div>
          <p>LP: {{ index + 1 }}</p>
          <p>Typ: {{ wagonType }}</p>
          <p>Osi: {{ axis }}</p>
          <p>Tara wagonu: {{ wagonTare }} kg</p>
          <p>Granica obciążenia: {{ maxPayload }} ton</p>
        </div>

        <span> {{ wagonNumber }}</span>
        <button
          class="rounded-lg border-2 px-4 text-red-400"
          @click="deleteWagon(index)"
        >
          Usuń
        </button>
        <div class="border-2 flex space-x-6">
          <label for="containerType">Rozmiar:</label>
          <select
            ref="containerType"
            :id="`containerType${index}`"
            class="text-black"
          >
            <option value="20DV">20DV</option>
            <option value="40HC" selected>40HC</option>
            <option value="40DV">40DV</option>
            <option value="45HC">45HC</option>
          </select>
        </div>

        <div class="border-2 flex space-x-6">
          <label for="emptyOrFull">Rozmiar:</label>
          <select
            ref="emptyOrFull"
            :id="`emptyOrFull${index}`"
            class="text-black"
          >
            <option value="pusty" selected>Pusty</option>
            <option value="ładowny">Ładowny</option>
          </select>
        </div>

        <label :for="`container${index}`">Wpisz numer kontenera</label>
        <input
          @input="checkLength"
          @keyup.enter="addContainer(index, wagons)"
          class="text-black h-12 text-xs placeholder-gray-400"
          maxlength="11"
          :id="`container${index}`"
          :ref="`containerInput${index}`"
          placeholder="nr kontenera"
        />
        <button
          class="rounded-lg border-2 px-4 "
          @click="addContainer(index, wagons)"
        >
          Dodaj kontener
        </button>
        <ul class="flex">
          <li
            class="border-2 border-gray-900 p-2"
            v-for="({ containerNumber, containerType, emptyOrFull, weight },
            idContainer) in wagons[index].kontenery"
            :key="idContainer"
          >
            <p>{{ containerNumber }}</p>
            <p>{{ containerType }}</p>
            <p>{{ emptyOrFull }}</p>
            <div class="flex flex-col space-y-2" v-if="emptyOrFull === full">
              <input
                @keyup.enter="
                  addSeal(wagons, index, idContainer, wagons[index].kontenery)
                "
                :id="`seal${index}${idContainer}`"
                class="text-black h-6 text-xs placeholder-gray-400"
                type="text"
                placeholder="plomba /ENTER"
              />
              <ul>
                <li
                  v-for="(seal, sealIndex) in wagons[index].kontenery[
                    idContainer
                  ].seals"
                  :key="sealIndex"
                >
                  plomba: {{ seal }}
                </li>
              </ul>
              <input
                @keyup.enter="
                  addWeight(wagons, index, idContainer, wagons[index].kontenery)
                "
                :id="`weight${index}${idContainer}`"
                class="text-black h-6 text-xs placeholder-gray-400"
                type="text"
                placeholder="waga w KG/ ENTER"
              />
              <p v-if="weight">Waga towaru: {{ weight }} kg</p>
            </div>
          </li>
        </ul>
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
      full: "ładowny",
    };
  },
  methods: {
    addWagon() {
      const wagonNumber = this.$refs.wagonInput.value;
      const wagonType = this.$refs.type.value;
      const wagonNormalLength = 12;
      let axis = null;
      let wagonTare = null;
      let maxPayload = null;

      if (
        wagonNumber.length !== wagonNormalLength ||
        this.wagons.some((element) =>
          element.wagonNumber === wagonNumber ? true : false
        )
      ) {
        this.wrongNumber = true;
        // console.log(this.$refs.type.value);
        return;
      } else {
        switch (wagonType) {
          case "kgns":
            axis = 2;
            wagonTare = 14000;
            maxPayload = 26;
            break;
          case "sgs":
            axis = 4;
            wagonTare = 21000;
            maxPayload = 58;
            break;
          case "sgns":
            axis = 4;
            wagonTare = 20000;
            maxPayload = 58;
            break;
          case "rgmms":
            axis = 4;
            wagonTare = 25000;
            maxPayload = 55;
            break;
          case "sdgmnss":
            axis = 4;
            wagonTare = 19500;
            maxPayload = 58;
            break;
          case "sggrss":
            axis = 6;
            wagonTare = 25100;
            maxPayload = 92;
            break;
          case "sggrs":
            axis = 6;
            wagonTare = 27100;
            maxPayload = 91;
            break;
          case "sggmrss":
            axis = 6;
            wagonTare = 28000;
            maxPayload = 88;
            break;
        }

        this.wagons.push({
          wagonNumber,
          wagonType,
          axis,
          wagonTare,
          maxPayload,
        });
        this.$refs.wagonInput.classList.remove("green");
        this.$refs.wagonInput.value = "";
        // console.log(this.wagons);
      }
    },
    deleteWagon(id) {
      this.wagons.splice(id, 1);
    },
    checkLength() {
      this.wrongNumber = false;
      if (this.$refs.wagonInput.value.length === 12) {
        this.$refs.wagonInput.classList.add("green");
      } else this.$refs.wagonInput.classList.remove("green");
    },
    addContainer(id, arr) {
      if (arr.indexOf(id)) {
        // console.log(id);
        const containerNumber = document.getElementById(`container${id}`).value;
        if (!containerNumber) {
          return;
        }
        const containerType = document.getElementById(`containerType${id}`)
          .value;
        const emptyOrFull = document.getElementById(`emptyOrFull${id}`).value;
        if (this.wagons[id].kontenery) {
          this.wagons[id].kontenery.push({
            containerNumber,
            containerType,
            emptyOrFull,
          });
          document.getElementById(`container${id}`).value = "";
        } else
          this.wagons[id].kontenery = [
            { containerNumber, containerType, emptyOrFull },
          ];
        document.getElementById(`container${id}`).value = "";
        // console.log(this.wagons);
      }
    },
    addSeal(wagonsArr, wagonsArrIndex, id, containersArr) {
      if (wagonsArr.indexOf(wagonsArrIndex)) {
        // console.log(`indeks wagonu ${wagonsArrIndex}`);
        if (containersArr.indexOf(id)) {
          // console.log(`to jest indeks kontenera ${id}`);
          const seal = document.getElementById(`seal${wagonsArrIndex}${id}`)
            .value;
          if (
            Object.prototype.hasOwnProperty.call(containersArr[id], "seals")
          ) {
            // console.log("on juz ma tablice z sealsami");
            containersArr[id].seals.push(seal);
            document.getElementById(`seal${wagonsArrIndex}${id}`).value = "";
            // console.log(containersArr[id].seals);
          } else {
            // console.log(seal);
            containersArr[id].seals = [seal];
            document.getElementById(`seal${wagonsArrIndex}${id}`).value = "";
            // console.log(containersArr[id].seals);
          }
        }
      }
    },
    addWeight(wagonsArr, wagonsArrIndex, id, containersArr) {
      if (wagonsArr.indexOf(wagonsArrIndex)) {
        if (containersArr.indexOf(id)) {
          const weight = document.getElementById(`weight${wagonsArrIndex}${id}`)
            .value;
          containersArr[id].weight = Number(weight);
          document.getElementById(`weight${wagonsArrIndex}${id}`).value = "";
          console.log(wagonsArr);
        }
      }
    },
  },
};
</script>

<style scoped>
.green {
  background-color: green;
}
</style>
