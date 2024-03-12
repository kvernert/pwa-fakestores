<script setup>
import ListagemProdutos from '@/components/ListagemProdutos.vue'
import RodaPe from '@/components/RodaPe.vue'
import RodaPeMobile from '@/components/RodaPeMobile.vue'
import { useScreen } from '@/composables/screen'

const {isMobile} = useScreen()
</script>

<template>
  <div>
    <ListagemProdutos />
    <RodaPe v-if="!isMobile" />
    <RodaPeMobile v-else class="mobile" />
  </div>
</template>
<style scoped></style>
