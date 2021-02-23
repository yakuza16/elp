<template>
  <div
    class="flex flex-col justify-items-center place-items-center space-y-4 my-10"
  >
    <button
      @click="generateXMLCode(payload)"
      class="border-2 rounded-lg p-2 border-white w-1/12"
    >
      XML
    </button>
    <label @click="copyXMLtext" class="pointer" for="xml">Skopiuj kod</label>
    <textarea
      @click="copyXMLtext"
      ref="xmlTextarea"
      name="xml"
      id="xml"
      cols="30"
      rows="10"
      class="w-2/3 text-white bg-gray-900"
    ></textarea>
  </div>
</template>

<script>
export default {
  data() {
    return {
      containerLengthCodes: {
        twentyFootCodeLength: 10,
        fortyFootHCCodeLength: 55,
        fotyFootDVCodeLength: 50,
      },
      containerTypes: {
        fortyFootHC: "40HC",
        fotyFootDV: "40DV",
        fourtyFive: "45HC",
        twentyFoot: "20DV",
      },
      containerWeight: {
        twentyFootWeight: 2200,
        fortyFootHCWeight: 4000,
        fotyFootDVWeight: 3700,
      },
      emptyOrFullCodes: {
        empty: 9931000000,
        full: 9941000000,
      },
    };
  },
  props: ["payload"],
  methods: {
    generateXMLCode(payload) {
      if (payload.length === 0) {
        return;
      } else {
        this.$refs.xmlTextarea.value = "";
        payload.forEach((element) => {
          const {
            axis,
            loadLength,
            kontenery,
            maxPayload,
            wagonNumber,
            wagonWeight,
          } = element;

          this.$refs.xmlTextarea.value += `<wagon>
      <number>${wagonNumber}</number>
      <mass>${wagonWeight}</mass>
      <maxWeight>${maxPayload}</maxWeight>
      <axis>${axis}</axis>
      <loadLength>${loadLength}</loadLength>${this.generateContainersXMLinfo(
            kontenery
          )}
      </wagon>`;
        });
      }
    },
    generateContainersXMLinfo(containersPayload) {
      let text = "";
      containersPayload.forEach((element) => {
        const {
          containerNumber,
          containerType,
          emptyOrFull,
          weight,
          seals,
        } = element;
        const { fortyFootHC, fotyFootDV, twentyFoot } = this.containerTypes;
        const { empty, full } = this.emptyOrFullCodes;
        const {
          twentyFootCodeLength,
          fortyFootHCCodeLength,
          fotyFootDVCodeLength,
        } = this.containerLengthCodes;
        const {
          twentyFootWeight,
          fortyFootHCWeight,
          fotyFootDVWeight,
        } = this.containerWeight;
        const generateCargoInfo = this.generateContainerCargoXMLInfo(
          weight,
          seals
        );
        const containersText = `
        <uti>
        <kind>1</kind>
         <codeLength>${
           containerType === fotyFootDV
             ? fotyFootDVCodeLength
             : containerType.includes(twentyFoot)
             ? twentyFootCodeLength
             : fortyFootHCCodeLength
         }</codeLength>
        <number>${containerNumber}</number>
        <code>${emptyOrFull === "pusty" ? empty : full}</code>
        <mass>${
          containerType === fortyFootHC
            ? fortyFootHCWeight
            : containerType.includes(twentyFoot)
            ? twentyFootWeight
            : fotyFootDVWeight
        }</mass>${emptyOrFull === "pusty" ? "".trim() : generateCargoInfo}
        </uti>`;
        return (text += containersText);
      });
      return text;
    },
    generateContainerCargoXMLInfo(cargoWeight, seals) {
      if (!seals) {
        return;
      } else {
        return `
      <cargo>
          <commodity>
            <NHM>9902000000</NHM>
          </commodity><massDeclaredByConsignor>${cargoWeight}</massDeclaredByConsignor>
        </cargo>
          ${this.generateSealsXMLInfo(seals)}`;
      }
    },
    generateSealsXMLInfo(sealsList) {
      let signs = "";
      sealsList.forEach((seal) => {
        let sealText = `<seal>
        <number>1</number>
        <signs>${seal}</signs>
        </seal>`;
        return (signs += sealText);
      });
      return signs;
    },
    copyXMLtext() {
      this.$refs.xmlTextarea.select();
      document.execCommand("copy");
    },
  },
};
</script>

<style></style>
