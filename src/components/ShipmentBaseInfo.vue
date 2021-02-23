<template>
  <div class="flex mb-10 place-content-center text-sm">
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
      <button @click="show">EEEE</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
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
      },
    };
  },
  methods: {
    show() {
      console.log(this.shipmentInfo.receiver.sindingDestinationStation());
    },
  },
};
</script>

<style></style>
