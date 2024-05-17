<script setup lang="ts">
const items = [
  "Home",
  "Perdidos e Achados",
  "Inspector Max",
  "Rick & Morty",
  "Sobre Nós",
  "Quem Somos",
  "Contato",
  "Login",
  "Cadastro",
  "Sair",
  "Carrinho",
  "Minha Conta",
  "Meus Pedidos",
  "Meus Dados",
];

onMounted(() => {
  const navItems = document.querySelectorAll("[data-nav-item]");
  if (navItems.length === 0) return;

  const firstY = navItems[0].getBoundingClientRect().y;
  navItems.forEach((item) => {
    const y = item.getBoundingClientRect().y;
    if (y !== firstY) {
      item.style.display = "none";
    }
  });
});
</script>

<template>
  <ul class="flex flex-wrap rounded bg-gray-100 gap-2 p-2 justify-center">
    <li v-for="item in items" data-nav-item class="p-2 bg-slate-300">
      {{ item }}
    </li>
  </ul>
</template>
