<template>
  <p class="text-lg font-bold border-t-2 pt-2">
    3. Wygeneruj kod XML i skopiuj go
  </p>
  <div
    class="flex flex-col justify-items-center place-items-center space-y-4 my-10"
  >
    <button @click="generateXMLCode(payload)" class="w-20">
      <img src="../assets/icons/xmlIcon.svg" alt="generateXML" />
    </button>
    <label
      @click="copyXMLtext"
      class="cursor-pointer rounded-md border-2 p-2 border-black bg-green-500"
      for="xml"
      ><img src="../assets/icons/copy.svg" alt="copy" class="w-6"
    /></label>

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
  <p class="text-lg font-bold mb-8">
    4. Skopiowany kod XML wklej do notatnika i zapisz go z rozszerzeniem .xml po
    czym zaczytaj plik w systemie ELP. Lub
    <a @click="downloadXML" ref="downloadXML" class="text-green-500"
      >Pobierz plik xml klikając tu</a
    >
  </p>
</template>

<script>
export default {
  props: ["payload", "shipment"],
  data() {
    return {
      containerLengthCodes: {
        twentyFootCodeLength: 10,
        fortyFootHCCodeLength: 55,
        fotyFootDVCodeLength: 50,
        shipment: this.$props.shipment,
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

  methods: {
    downloadXML() {
      const blob = new Blob([this.$refs.xmlTextarea.value], {
        type: "text/xml",
      });
      console.log(blob);
      this.$refs.downloadXML.href = window.URL.createObjectURL(blob);
      this.$refs.downloadXML.download = "elp.xml";
    },
    generateXMLCode(payload) {
      if (payload.length === 0 || !this.shipment) {
        return;
      } else {
        this.$refs.xmlTextarea.value = this.shipment;
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
        this.$refs.xmlTextarea.value += `
  </wagons>
  <paying>
    <agreementNumber></agreementNumber>
    <payer>
      <identifier>
        <identifier></identifier>
      </identifier>
    </payer>
    <code>31</code>
  </paying>
  <statements>
    <consignorStatement>
      <statement>025</statement>
      <statementContent>Towar do dalszego wywozu drogą wodną do CHINY (kraj).</statementContent>
      <data>Chiny</data>
    </consignorStatement>
    <consignorStatement>
      <statement>035</statement>
      <statementContent>Przesyłka nadzwyczajna. Zgoda nr PNK PNZ0-019-2021 z dnia</statementContent>
      <data>PNK PNZ0-019-2021</data>
    </consignorStatement>
    <consignorStatement>
      <statement>015</statement>
      <statementContent></statementContent>
      <data></data>
    </consignorStatement>
    <consignorStatement>
      <statement>005</statement>
      <statementContent>Umowa handlowa nr </statementContent>
    </consignorStatement>
    <consignorStatementsNotAplicable>
      <consignorStatementsNotAplicable>KONTENERY WIELOKROTNEGO UŻYTKU, POSIADAJĄ LICZNE WGNIECENIA, ZARYSOWANIA I ŚLADY RDZY.</consignorStatementsNotAplicable>
    </consignorStatementsNotAplicable>
  </statements>
</ns2:shipment>`;
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
