<script setup lang="ts">
const maxLength = 5;
const maxDecimal = 2;

function handleInputChange(e: Event) {
  e.preventDefault();
  const input = e.target as HTMLInputElement;
  const [integerPart, decimalPart] = input.value.split(".");

  if(integerPart.length === 0){
    return;
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
  <input type="number" @input="handleInputChange" class="border px-1 py-2" />
</template>
