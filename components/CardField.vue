<script setup lang="ts">
interface BpmData {
  id: string;
  parent: string;
  data: {
    imageUri: string;
    text: string;
    link: string;
  }[];
}

const props = defineProps<{
  name: string;
  dataUri: string;
}>();

const {
  pending,
  data: { value },
  error,
} = await useFetch(props.dataUri, {
  lazy: true,
});

const cardData = value as BpmData;
</script>

<template>
  <div class="bg-gray-100 p-4 rounded">
    <div v-if="error" class="text-red-500">{{ error.message }}</div>
    <div v-else-if="pending" class="text-gray-500">Loading...</div>
    <div v-else class="grid grid-cols-1 sm:grid-cols-3 gap-4">
      <div v-for="item in cardData.data" class="border border-gray-200 rounded">
        <img :src="item.imageUri" alt="" class="w-full" />
      </div>
    </div>
  </div>
</template>
