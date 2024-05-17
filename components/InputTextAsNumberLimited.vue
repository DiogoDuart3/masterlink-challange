<script setup lang="ts">
const maxLength = 5;
const maxDecimal = 2;

function handleInputChange(e: Event) {
  e.preventDefault();
  const input = e.target as HTMLInputElement;
  const inputValueFiltered = input.value.replace(/,/g, '.').replace(/[^0-9.]/g, "");
  const [integerPart, decimalPart] = inputValueFiltered.split(".");

  if(integerPart.length === 0){
    return input.value = '';
  }

  let newValue = integerPart;
  console.log(integerPart, decimalPart);

  if (decimalPart !== undefined) {
    newValue += "." + decimalPart.slice(0, maxDecimal);
  }

  if (integerPart.length > maxLength) {
    newValue = integerPart.slice(0, maxLength) + (decimalPart ? '.' + decimalPart.slice(0, maxDecimal) : '');
  }

  input.value = newValue;
}
</script>

<template>
  <input type="text" @input="handleInputChange" class="border px-1 py-2" />
</template>
