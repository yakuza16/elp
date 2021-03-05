<template>
  <div class="border-b-2 py-2">
    <div id="inputsParentWrapper" class="flex mb-10 place-content-center">
      <div class="w-1/3 p-4 flex flex-col place-items-end">
        <h1>Nadawca</h1>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consignorRegon">REGON</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consignorRegon"
            ref="senderRegon"
          />
        </div>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consignorCompanyName">Nazwa firmy</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consignorCompanyName"
            ref="senderCompany"
          />
        </div>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consignorNIP">NIP</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consignorNIP"
            ref="senderNip"
          />
        </div>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consignorStreet">Ulica</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consignorStreet"
            ref="senderStreet"
          />
        </div>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consignorCity">Miasto</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consignorCity"
            ref="senderCity"
          />
        </div>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consignorPostalCode">Kod pocztowy</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consignorPostalCode"
            ref="senderPostalCode"
          />
        </div>
        <div class="flex bg-gray-700">
          <div class="border-2 flex p-1 place-items-center space-x-1">
            <label for="dispatchStation">Kod stacji nadania</label>
            <input
              class="text-black h-8 text-xs placeholder-gray-400 p-1"
              type="text"
              id="dispatchStation"
              ref="dispatchStationCode"
            />
          </div>
          <div class="border-2 flex p-1 place-items-center space-x-1">
            <label for="sindingDispatchStation"
              >Miejsce podstawienia na stacji nadania</label
            >
            <input
              class="text-black h-8 text-xs placeholder-gray-400 p-1"
              type="text"
              id="sindingDispatchStation"
              ref="sindingDispatchStation"
            />
          </div>
        </div>
      </div>
      <div class="w-1/3 p-4 flex flex-col place-items-end">
        <h1>Odbiorca</h1>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consigneeRegon">REGON</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consigneeRegon"
            ref="receiverRegon"
          />
        </div>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consigneeCompanyName">Nazwa firmy</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consigneeCompanyName"
            ref="receiverCompany"
          />
        </div>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consigneeNIP">NIP</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consigneeNIP"
            ref="receiverNip"
          />
        </div>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consigneeStreet">Ulica</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consigneeStreet"
            ref="receiverStreet"
          />
        </div>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consigneeCity">Miasto</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consigneeCity"
            ref="receiverCity"
          />
        </div>
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="consigneePostalCode">Kod pocztowy</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="consigneePostalCode"
            ref="receiverPostalCode"
          />
        </div>
        <div class="flex bg-gray-700">
          <div class="border-2 flex p-1 place-items-center space-x-1">
            <label for="destinationStation">Kod stacji odbioru</label>
            <input
              class="text-black h-8 text-xs placeholder-gray-400 p-1"
              type="text"
              id="destinationStation"
              ref="destinationStationCode"
            />
          </div>
          <div class="border-2 flex p-1 place-items-center space-x-1">
            <label for="sindingDestinationStation"
              >Miejsce podstawienia na stacji odbioru</label
            >
            <input
              class="text-black h-8 text-xs placeholder-gray-400 p-1"
              type="text"
              id="sindingDestinationStation"
              ref="sindingDestinationStation"
            />
          </div>
        </div>
      </div>
    </div>
    <button
      class="rounded-lg border-2 px-4 py-1 w-14 "
      :class="[isEditable ? locked : unlocked]"
      ref="acceptShipment"
      @click="saveShipmentInfo"
    >
      <img
        v-show="isEditable"
        class="w-full"
        src="../assets/icons/open-lock.svg"
        alt="lock"
      />
      <img
        v-show="!isEditable"
        class="w-full"
        src="../assets/icons/closed-lock.svg"
        alt="lock"
      />
    </button>
  </div>
</template>

<script>
export default {
  emits: ["createShipmentInfo"],
  data() {
    return {
      locked: "bg-red-500",
      unlocked: "bg-green-500",
      isEditable: true,
      shipmentInfo: {
        sender: {
          regon: () => this.$refs.senderRegon.value,
          company: () => this.$refs.senderCompany.value,
          nip: () => this.$refs.senderNip.value,
          street: () => this.$refs.senderStreet.value,
          city: () => this.$refs.senderCity.value,
          postalCode: () => this.$refs.senderPostalCode.value,
          dispatchStation: () => this.$refs.dispatchStationCode.value,
          sindingDispatchStation: () => this.$refs.sindingDispatchStation.value,
        },
        receiver: {
          regon: () => this.$refs.receiverRegon.value,
          company: () => this.$refs.receiverCompany.value,
          nip: () => this.$refs.receiverNip.value,
          street: () => this.$refs.receiverStreet.value,
          city: () => this.$refs.receiverCity.value,
          postalCode: () => this.$refs.receiverPostalCode.value,
          destinationStation: () => this.$refs.destinationStationCode.value,
          sindingDestinationStation: () =>
            this.$refs.sindingDestinationStation.value,
        },
        shipmentInfoXML: null,
      },
    };
  },
  methods: {
    generateShipmentInformations() {
      const shipmentInfo = `<?xml version="1.0"?>
<ns2:shipment xmlns:ns3="http://www.pkp-cargo.pl/elpext" xmlns:ns2="http://www.pkp-cargo.pl/elp">
      <shipmentBaseInfo>
    <group>True</group>
    <kind>country</kind>
    <type>UTI</type>
    <consignor>
      <identifier>
        <countryCode>PL</countryCode>
        <identifier>${this.shipmentInfo.sender.regon()}</identifier>
        <organizationalUnit>1</organizationalUnit>
      </identifier>
      <name>${this.shipmentInfo.sender.company()}</name>
      <NIP>${this.shipmentInfo.sender.nip()}</NIP>
      <address>
        <street>${this.shipmentInfo.sender.street()}</street>
        <city>${this.shipmentInfo.sender.city()}</city>
        <postalCode>${this.shipmentInfo.sender.postalCode()}</postalCode>
      </address>
      <contact />
    </consignor>
    <consignee>
      <identifier>
        <countryCode>PL</countryCode>
        <identifier>${this.shipmentInfo.receiver.regon()}</identifier>
      </identifier>
      <name>${this.shipmentInfo.receiver.company()}</name>
      <NIP>${this.shipmentInfo.receiver.nip()}</NIP>
      <address>
        <street>${this.shipmentInfo.receiver.street()}</street>
        <city>${this.shipmentInfo.receiver.city()}</city>
        <postalCode>${this.shipmentInfo.receiver.postalCode()}</postalCode>
      </address>
      <contact />
    </consignee>
    <dispatchStation>
      <administration>51</administration>
      <stationCode>${this.shipmentInfo.sender.dispatchStation()}</stationCode>
      <siding>${this.shipmentInfo.sender.sindingDispatchStation()}</siding>
    </dispatchStation>
    <destinationStation>
      <administration>51</administration>
      <stationCode>${this.shipmentInfo.receiver.destinationStation()}</stationCode>
      <siding>${this.shipmentInfo.receiver.sindingDestinationStation()}</siding>
    </destinationStation>
    <registrationMethod>X</registrationMethod>
  </shipmentBaseInfo>
  <wagons>
      `;
      return shipmentInfo;
    },
    saveShipmentInfo() {
      const shipmentInputsParent = document.getElementById(
        "inputsParentWrapper"
      );
      const allShipmentInputs = shipmentInputsParent.getElementsByTagName(
        "input"
      );
      if (this.isEditable === true) {
        allShipmentInputs.forEach((input) => {
          input.setAttribute("disabled", true);
          this.shipmentInfoXML = this.generateShipmentInformations();
          this.isEditable = false;
          this.onClickButton();
        });
      } else {
        this.isEditable = true;
        allShipmentInputs.forEach((input) => {
          input.removeAttribute("disabled");
        });
      }
    },
    onClickButton() {
      this.$emit("createShipmentInfo", this.shipmentInfoXML);
    },
  },
};
</script>

<style></style>
