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
  props: ["payload"],
  methods: {
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
        // console.log(containersPayload, element, index, arr);
        const { containerNumber, containerType, emptyOrFull } = element;
        // console.log(containerNumber, containerType);
        const containersText = `
        <uti>
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
        console.log(containersText);
        return (text += containersText);
      });
      return text;
    },
  },
};
</script>

<style></style>
