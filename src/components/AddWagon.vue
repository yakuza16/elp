<template>
  <div class="flex justify-start space-x-4 place-items-center text-xs ml-3">
    <div class="border-2 p-1 flex space-x-1 place-items-center">
      <label for="type">Typ wagonu:</label>
      <select ref="type" id="type" class="h-8 text-black">
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
    <div class="border-2 flex p-1 place-items-center space-x-1">
      <label for="wagon">Wpisz numer wagonu</label>
      <input
        @input="checkWagonLength"
        @keyup.enter="addWagon"
        class="text-black h-8 text-xs placeholder-gray-400 p-1"
        maxlength="12"
        id="wagon"
        ref="wagonInput"
        placeholder="nr wagonu"
      />
    </div>
    <button
      class="rounded-lg border-2 px-4 py-1 w-14 bg-green-500"
      @click="addWagon"
    >
      <img src="../assets/icons/add.svg" alt="add" />
    </button>
    <span class="text-red-500" v-show="isWagonNumberTooShort"
      >Wpisałeś za krótki nr wagonu lub próbujesz dodać ponownie ten sam
      wagon</span
    >
  </div>
  <div class="flex text-xs">
    <ul class="flex flex-col my-4">
      <li
        class="flex justify-start place-items-center space-x-2 my-1 ml-3 border-black border-2"
        v-for="({ wagonNumber, wagonType, axis, wagonWeight, maxPayload },
        index) in wagons"
        :key="index"
      >
        <div class="text-left px-2">
          <p>
            LP: <span class="text-green-400">{{ index + 1 }}</span>
          </p>
          <p>
            Typ: <span class="text-green-400">{{ wagonType }}</span>
          </p>
          <p>
            Osi: <span class="text-green-400">{{ axis }}</span>
          </p>
          <p>
            Tara wagonu:
            <span class="text-green-400">{{ wagonWeight }} kg</span>
          </p>
          <p>
            Granica obciążenia:
            <span class="text-green-400">{{ maxPayload }} ton</span>
          </p>
        </div>
        <input
          class="text-green-400 text-lg font-bold bg-transparent w-36 p-1"
          type="text"
          :value="wagonNumber"
          maxlength="12"
          readonly
          :id="`wagonNumber${index}`"
        />
        <div class="flex flex-col space-y-2">
          <button
            class="rounded-lg border-2 px-4 py-1 bg-gray-500 w-12"
            @click="editWagon(index)"
          >
            <img src="../assets/icons/pen.svg" alt="delete" />
          </button>
          <button
            class="rounded-lg border-2 px-4 py-1 bg-red-500 w-12"
            @click="deleteWagon(index)"
          >
            <img src="../assets/icons/trash.svg" alt="delete" />
          </button>
        </div>

        <div class="border-2 p-1 flex space-x-1 place-items-center">
          <label :for="`containerType${index}`">Rozmiar:</label>
          <select
            ref="containerType"
            :id="`containerType${index}`"
            class="h-8 text-black"
          >
            <option value="20DV">20DV</option>
            <option value="40HC" selected>40HC</option>
            <option value="40DV">40DV</option>
            <option value="45HC">45HC</option>
          </select>
        </div>

        <div class="border-2 p-1 flex space-x-1 place-items-center">
          <label :for="`emptyOrFull${index}`">Rozmiar:</label>
          <select
            ref="emptyOrFull"
            :id="`emptyOrFull${index}`"
            class="h-8 text-black"
          >
            <option value="pusty" selected>Pusty</option>
            <option value="ładowny">Ładowny</option>
          </select>
        </div>

        <label :for="`container${index}`">Wpisz numer kontenera</label>
        <input
          @keyup.enter="addContainer(index, wagons)"
          class="text-black h-8 text-xs placeholder-gray-400 w-24 p-1"
          maxlength="11"
          :id="`container${index}`"
          :ref="`containerInput${index}`"
          placeholder="nr kontenera"
        />
        <button
          class="rounded-lg border-2 px-4 py-1 bg-green-500 w-12 "
          @click="addContainer(index, wagons)"
        >
          <img src="../assets/icons/add.svg" alt="add" />
        </button>
        <ul class="flex place-items-center p-1 space-x-2">
          <li
            class="border-2 border-green-500 p-1 w-48"
            v-for="({ containerNumber, containerType, emptyOrFull, weight },
            idContainer) in wagons[index].kontenery"
            :key="idContainer"
          >
            <div
              class="flex flex-col justify-items-center place-items-center space-y-1 my-1"
            >
              <p class="text-base font-bold">
                <span>{{ containerType }}</span>
                {{ containerNumber }}
              </p>
              <p class="text-green-400 font-bold">{{ emptyOrFull }}</p>
              <button
                @click="
                  deleteContainer(
                    wagons,
                    index,
                    wagons[index].kontenery,
                    idContainer
                  )
                "
                class="rounded-lg border-2 px-4 py-1 bg-red-500 w-12 place-self-end"
              >
                <img src="../assets/icons/trash.svg" alt="delete container" />
              </button>
            </div>
            <div
              class="flex flex-col space-y-4 place-items-center"
              v-if="emptyOrFull === full"
            >
              <input
                @keyup.enter="
                  addSeal(wagons, index, idContainer, wagons[index].kontenery)
                "
                :id="`seal${index}${idContainer}`"
                class="text-black h-6 text-xs placeholder-gray-400 w-20 mt-2 p-1"
                type="text"
                placeholder="plomba"
              />
              <ul>
                <li
                  class="text-left"
                  v-for="(seal, sealIndex) in wagons[index].kontenery[
                    idContainer
                  ].seals"
                  :key="sealIndex"
                >
                  plomba: <span class="text-green-400"> {{ seal }}</span>
                </li>
              </ul>
              <input
                @keyup.enter="
                  addWeight(wagons, index, idContainer, wagons[index].kontenery)
                "
                :id="`weight${index}${idContainer}`"
                class="text-black h-6 text-xs placeholder-gray-400 w-20 p-1"
                type="text"
                placeholder="waga KG"
              />
              <p class="flex flex-col justify-items-center place-items-center">
                Waga towaru:
                <span class="text-green-400"> {{ weight }} </span> kg
                <span v-if="Number(weight) > 28000">
                  <img src="../assets/icons/warn.svg" alt="warning" />
                </span>
              </p>
            </div>
          </li>
        </ul>
      </li>
    </ul>
  </div>
  <div
    class="flex flex-col justify-items-center place-items-center space-y-4 my-10"
  >
    <button
      @click="generateXMLCode(wagons)"
      class="border-2 rounded-lg p-2 border-white w-1/12"
    >
      XML
    </button>
    <label class="pointer" for="xml">Skopiuj kod</label>
    <textarea
      ref="xmlTextarea"
      name="xml"
      id="xml"
      cols="30"
      rows="10"
      class="w-1/3 text-white bg-gray-900"
    ></textarea>
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
      isWagonNumberTooShort: false,
      isContainerNumberTooShort: false,
      full: "ładowny",
      wagonPositiveLength: 12,
      containerPositiveLength: 11,
    };
  },
  methods: {
    addWagon() {
      const wagonNumber = this.$refs.wagonInput.value;
      const wagonType = this.$refs.type.value;
      let axis = null;
      let wagonWeight = null;
      let maxPayload = null;
      let loadLength = null;

      if (
        wagonNumber.length !== this.wagonPositiveLength ||
        this.wagons.some((element) =>
          element.wagonNumber === wagonNumber ? true : false
        )
      ) {
        this.isWagonNumberTooShort = true;
        return;
      } else {
        switch (wagonType) {
          case "kgns":
            axis = 2;
            wagonWeight = 14000;
            maxPayload = 26;
            loadLength = 40;
            break;
          case "sgs":
            axis = 4;
            wagonWeight = 21000;
            maxPayload = 58;
            loadLength = 60;
            break;
          case "sgns":
            axis = 4;
            wagonWeight = 20000;
            maxPayload = 58;
            loadLength = 60;
            break;
          case "rgmms":
            axis = 4;
            wagonWeight = 25000;
            maxPayload = 55;
            loadLength = 40;
            break;
          case "sdgmnss":
            axis = 4;
            wagonWeight = 19500;
            maxPayload = 58;
            loadLength = 60;
            break;
          case "sggrss":
            axis = 6;
            wagonWeight = 25100;
            maxPayload = 92;
            loadLength = 80;
            break;
          case "sggrs":
            axis = 6;
            wagonWeight = 27100;
            maxPayload = 91;
            loadLength = 80;
            break;
          case "sggmrss":
            axis = 6;
            wagonWeight = 28000;
            maxPayload = 88;
            loadLength = 80;
            break;
        }

        this.wagons.push({
          wagonNumber,
          wagonType,
          axis,
          wagonWeight,
          maxPayload,
          loadLength,
          kontenery: [],
        });
        this.$refs.wagonInput.classList.remove("green");
        this.$refs.wagonInput.value = "";
      }
    },
    deleteWagon(id) {
      this.wagons.splice(id, 1);
    },
    editWagon(id) {
      const wagonToEdit = document.getElementById(`wagonNumber${id}`);
      if (!wagonToEdit) {
        console.log(`cant find element with ${id}`);
      } else {
        if (wagonToEdit.hasAttribute("readonly")) {
          wagonToEdit.removeAttribute("readonly");
          wagonToEdit.classList.add("bg-gray-300");
        } else {
          if (
            wagonToEdit.value.length !== this.wagonPositiveLength ||
            this.wagons.some((element) =>
              element.wagonNumber === wagonToEdit.value ? true : false
            )
          ) {
            this.isWagonNumberTooShort = true;
            this.wagons[id].wagonNumber = "";
          } else {
            this.isWagonNumberTooShort = false;
            wagonToEdit.setAttribute("readonly", "true");
            wagonToEdit.classList.remove("bg-gray-300");
            this.wagons[id].wagonNumber = wagonToEdit.value;
            console.log(this.wagons);
          }
        }
      }
    },
    deleteContainer(wagons, idWagons, containers, idContainer) {
      if (wagons.indexOf(idWagons)) {
        if (containers.indexOf(idContainer)) {
          this.wagons[idWagons].kontenery.splice(idContainer, 1);
        }
      }
    },
    checkWagonLength() {
      this.isWagonNumberTooShort = false;
      if (this.$refs.wagonInput.value.length === this.wagonPositiveLength) {
        this.$refs.wagonInput.classList.add("green");
      } else this.$refs.wagonInput.classList.remove("green");
    },
    addContainer(id, arr) {
      if (arr.indexOf(id)) {
        const containerNumber = document.getElementById(`container${id}`).value;
        if (
          !containerNumber ||
          containerNumber.length !== this.containerPositiveLength
        ) {
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
      }
    },
    addSeal(wagonsArr, wagonsArrIndex, id, containersArr) {
      if (wagonsArr.indexOf(wagonsArrIndex)) {
        if (containersArr.indexOf(id)) {
          const seal = document.getElementById(`seal${wagonsArrIndex}${id}`)
            .value;
          if (
            Object.prototype.hasOwnProperty.call(containersArr[id], "seals")
          ) {
            containersArr[id].seals.push(seal);
            document.getElementById(`seal${wagonsArrIndex}${id}`).value = "";
          } else {
            containersArr[id].seals = [seal];
            document.getElementById(`seal${wagonsArrIndex}${id}`).value = "";
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
        }
      }
    },
    generateXMLCode(payload) {
      if (payload.length === 0) {
        return;
      } else {
        this.$refs.xmlTextarea.value = "";
        // this.$refs.xmlTextarea.value = "hej";
        // console.log(payload);
        payload.forEach((element) => {
          // console.log(element, index, array);
          const {
            axis,
            loadLength,
            kontenery,
            maxPayload,
            wagonNumber,
            wagonWeight,
          } = element;

          this.$refs.xmlTextarea.value += `
      <wagon>
      <number>${wagonNumber}</number>
      <mass>${wagonWeight}</mass>
      <maxWeight>${maxPayload}</maxWeight>
      <axis>${axis}</axis>
      <loadLength>${loadLength}</loadLength>
      ${this.generateContainersXMLinfo(kontenery)}
      </wagon>`;
        });
      }
    },
    generateContainersXMLinfo(containersPayload) {
      containersPayload.forEach((element) => {
        // console.log(containersPayload, element, index, arr);
        const { containerNumber, containerType, emptyOrFull } = element;
        // console.log(containerNumber, containerType);
        const containersText = `<uti>
        <kind>1</kind>
         <codeLength>${
           containerType === "40HC"
             ? 55
             : containerType.includes("20")
             ? 10
             : 50
         }</codeLength>
        <number>${containerNumber}</number>
        <code>${emptyOrFull === "pusty" ? 9931000000 : 9941000000}</code>
        <mass>${
          containerType === "40HC"
            ? 3900
            : containerType.includes("20")
            ? 2200
            : 9700
        }</mass>
        </uti>`;
        return containersText;
      });
    },
  },
};
</script>

<style scoped>
.green {
  background-color: rgb(52, 211, 153);
}

input:focus,
select:focus {
  outline-color: rgb(52, 211, 153);
  outline-offset: 2px;
}
</style>
