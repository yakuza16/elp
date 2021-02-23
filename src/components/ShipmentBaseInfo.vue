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
        />
      </div>
      <div class="border-2 flex p-1 place-items-center space-x-1">
        <label for="consignorCompanyName">Nazwa firmy</label>
        <input
          class="text-black h-8 text-xs placeholder-gray-400 p-1"
          type="text"
          id="consignorCompanyName"
        />
      </div>
      <div class="border-2 flex p-1 place-items-center space-x-1">
        <label for="consignorNIP">NIP</label>
        <input
          class="text-black h-8 text-xs placeholder-gray-400 p-1"
          type="text"
          id="consignorNIP"
        />
      </div>
      <div class="border-2 flex p-1 place-items-center space-x-1">
        <label for="consignorStreet">Ulica</label>
        <input
          class="text-black h-8 text-xs placeholder-gray-400 p-1"
          type="text"
          id="consignorStreet"
        />
      </div>
      <div class="border-2 flex p-1 place-items-center space-x-1">
        <label for="consignorCity">Miasto</label>
        <input
          class="text-black h-8 text-xs placeholder-gray-400 p-1"
          type="text"
          id="consignorCity"
        />
      </div>
      <div class="border-2 flex p-1 place-items-center space-x-1">
        <label for="consignorPostalCode">Kod pocztowy</label>
        <input
          class="text-black h-8 text-xs placeholder-gray-400 p-1"
          type="text"
          id="consignorPostalCode"
        />
      </div>
      <div class="flex bg-gray-700">
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="dispatchStation">Kod stacji nadania</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="dispatchStation"
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
        />
      </div>
      <div class="border-2 flex p-1 place-items-center space-x-1">
        <label for="consigneeCompanyName">Nazwa firmy</label>
        <input
          class="text-black h-8 text-xs placeholder-gray-400 p-1"
          type="text"
          id="consigneeCompanyName"
        />
      </div>
      <div class="border-2 flex p-1 place-items-center space-x-1">
        <label for="consigneeNIP">NIP</label>
        <input
          class="text-black h-8 text-xs placeholder-gray-400 p-1"
          type="text"
          id="consigneeNIP"
        />
      </div>
      <div class="border-2 flex p-1 place-items-center space-x-1">
        <label for="consigneeStreet">Ulica</label>
        <input
          class="text-black h-8 text-xs placeholder-gray-400 p-1"
          type="text"
          id="consigneeStreet"
        />
      </div>
      <div class="border-2 flex p-1 place-items-center space-x-1">
        <label for="consigneeCity">Miasto</label>
        <input
          class="text-black h-8 text-xs placeholder-gray-400 p-1"
          type="text"
          id="consigneeCity"
        />
      </div>
      <div class="border-2 flex p-1 place-items-center space-x-1">
        <label for="consigneePostalCode">Kod pocztowy</label>
        <input
          class="text-black h-8 text-xs placeholder-gray-400 p-1"
          type="text"
          id="consigneePostalCode"
        />
      </div>
      <div class="flex bg-gray-700">
        <div class="border-2 flex p-1 place-items-center space-x-1">
          <label for="destinationStation">Kod stacji odbioru</label>
          <input
            class="text-black h-8 text-xs placeholder-gray-400 p-1"
            type="text"
            id="destinationStation"
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
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style></style>
