<script setup lang="ts">
type FieldType = "text" | "password" | "int" | "card";

interface Metadata {
  id: string;
  title: string;
  fields: {
    id: string;
    type: FieldType;
    name: string;
    dataUri?: string;
  }[];
}

const {
  pending,
  data: { value },
  error,
} = await useFetch("https://masterlink-mock-api.mwe.pt/MlkApi/bpm_metadata/1", {
  lazy: true,
});
const metadata = value as Metadata;
console.log(metadata);

function submit(e: Event) {
  e.preventDefault();
  alert(
    "Submitted, i don't have futher instructions \n The values are on the console"
  );

  const formData = new FormData(e.target as HTMLFormElement);
  const data = Object.fromEntries(formData.entries());
  console.log(data);
}
</script>

<template>
  <div class="p-12 mx-auto max-w-2xl">
    <h1
      class="bg-gradient-to-br from-red-400 to-indigo-400 inline-block text-transparent bg-clip-text font-bold uppercase text-3xl w-full text-center"
    >
      MasterLink challange
    </h1>
    <div class="mt-6">
      <div v-if="pending">
        <p>Loading...</p>
      </div>
      <div v-else-if="error">
        <p>Error: {{ error }}</p>
      </div>
      <div v-else>
        <h2 class="text-slate-700 font-semibold text-xl text-center">
          {{ metadata.title }}
        </h2>
        <form
          v-on:submit="submit"
          class="space-y-3 mt-2 border p-4 rounded border-gray-100"
        >
          <div v-for="field in metadata.fields" class="flex flex-col space-y-1">
            <label for="field.id">{{ field.name }}</label>
            <input
              v-if="field.type === 'text'"
              :name="field.id"
              class="bg-gray-200/50 rounded py-1 px-2 text-sm"
              required
            />
            <input
              v-if="field.type === 'password'"
              :name="field.id"
              type="password"
              class="bg-gray-200/50 rounded py-1 px-2 text-sm"
              required
            />
            <input
              v-if="field.type === 'int'"
              :name="field.id"
              type="number"
              class="bg-gray-200/50 rounded py-1 px-2 text-sm"
              required
            />
            <CardField
              v-if="field.type === 'card' && field.dataUri"
              :name="field.name"
              :data-uri="field.dataUri"
            />
          </div>
          <button
            type="submit"
            class="px-2 py-1 rounded bg-slate-200 text-gray-800"
          >
            Submeter
          </button>
        </form>
      </div>
    </div>
  </div>
</template>
