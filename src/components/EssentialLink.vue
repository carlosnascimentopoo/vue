<template>
  <!-- Se tem "to", é rota interna (SPA). Senão, link externo. -->
  <q-item
    v-if="to"
    clickable
    :to="to"
    exact
  >
    <q-item-section v-if="icon" avatar>
      <q-icon :name="icon" />
    </q-item-section>
    <q-item-section>
      <q-item-label>{{ label }}</q-item-label>
      <q-item-label caption>{{ caption }}</q-item-label>
    </q-item-section>
  </q-item>

  <q-item
    v-else
    clickable
    tag="a"
    target="_blank"
    :href="link"
  >
    <q-item-section v-if="icon" avatar>
      <q-icon :name="icon" />
    </q-item-section>
    <q-item-section>
      <q-item-label>{{ label }}</q-item-label>
      <q-item-label caption>{{ caption }}</q-item-label>
    </q-item-section>
  </q-item>
</template>

<script setup lang="ts">
export interface EssentialLinkProps {
  label: string;
  caption?: string;
  link?: string;
  to?: string;      // ← ADICIONE ISSO
  icon?: string;
}

withDefaults(defineProps<EssentialLinkProps>(), {
  caption: "",
  link: "#",
  to: "",
  icon: ""
});
</script>
