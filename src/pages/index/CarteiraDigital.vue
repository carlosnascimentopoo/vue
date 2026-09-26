<template>
  <section class="wrapper flex q-pa-lg">
  <div>
    <div>
      <h1>Carteira Digital</h1>
      <div class="flex q-gutter-lg">
        <div class="box-saldo bg-primary text-white q-pa-md rounded-borders-lg">
          <span>Saldo</span>
          <div>R$ 1000,00</div>
        </div>

        <div class="box-gastos bg-red text-white q-pa-md rounded-borders-md">
          <span>Gastos</span>
          <div>R$ 100,00</div>
        </div>

        <div class="box-receita bg-green text-white q-pa-md rounded-borders-md">
          <span>Receita</span>
          <div>R$ 1100,00</div>
        </div>
      </div>

      <div class="flex column q-gutter-md q-pt-md">
      <InputDados type="number" placeholder="R$" v-model="carteira.valor" />
      <InputDados
        type="text"
        placeholder="Descrição"
        v-model="carteira.descricao"
      />
      <InputDados type="text" placeholder="Tipo" v-model="carteira.tipo" />

      <q-btn label="adicionar transação" icon="add" color="primary" />
      </div>
    </div>
  </div>

  <div class="container-history">
    <h2>Histórico de transções</h2>
    <ul>
      <li class="flex q-gutter-lg border-bottom">
        <p>Lanche</p>
        <p>R$ 100,00</p>
        <div class="flex items-center">
          <q-btn color="red" size="sm" icon="delete"/>
          <q-btn color="orange" size="sm" icon="edit"/>
        </div>
       </li>
       <li class="flex border">
        <p>Lanche</p>
        <p>R$ 100,00</p>
        <div class="flex items-center">
          <q-btn color="red" size="sm" icon="delete"/>
          <q-btn color="orange" size="sm" icon="edit"/>
        </div>
       </li>
    </ul>
  </div>
</section>
</template>

<script setup lang="ts">
import { ref } from "vue";
import InputDados from "@/components/InputDados.vue";

interface Carteira {
  valor: number | null;
  descricao: string;
  tipo: string;
}

interface Transacao extends Carteira {
  id: number;
}

const carteira = ref<Carteira>({
  valor: null,
  descricao: "",
  tipo: ""
});

const transacoes = ref<Transacao[]>([
  {
    id: 1,
    valor: 100,
    descricao: "Comida de restaurante",
    tipo: "gasto"
  },
  {
    id: 2,
    valor: 300,
    descricao: "Lembrança",
    tipo: "gasto"
  }
]);
</script>


<style scoped>
.wrapper{
  border:2px solid red;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 35px;
  max-width:1024px;
  margin:0 auto;
}
</style>
