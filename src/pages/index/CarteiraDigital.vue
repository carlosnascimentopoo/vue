<template>
  <section class="wrapper flex q-pa-lg">
  <div>
    <div>
      <h1 class="title-wallet">Carteira Digital</h1>
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
    <h4 class="text-center text-bold">Histórico de transações</h4>
    <ul class="history">

      <li class="d-flex-history">
        <p>Supermercado</p>
        <p>R$ 300,00</p>
        <div class="flex items-cente q-gutter-sm">
          <q-btn color="red" size="sm" icon="delete"/>
          <q-btn color="orange" size="sm" icon="edit"/>
        </div>
       </li>

       <li class="d-flex-history">
        <p>Supermercado</p>
        <p>R$ 300,00</p>
        <div class="flex items-cente q-gutter-sm">
          <q-btn color="red" size="sm" icon="delete"/>
          <q-btn color="orange" size="sm" icon="edit"/>
        </div>
       </li>


       <li class="d-flex-history">
        <p>Supermercado</p>
        <p>R$ 300,00</p>
        <div class="flex items-cente q-gutter-sm">
          <q-btn color="red" size="sm" icon="delete"/>
          <q-btn color="orange" size="sm" icon="edit"/>
        </div>
       </li>

       <li class="d-flex-history">
        <p>Supermercado</p>
        <p>R$ 300,00</p>
        <div class="flex items-cente q-gutter-sm">
          <q-btn color="red" size="sm" icon="delete"/>
          <q-btn color="orange" size="sm" icon="edit"/>
        </div>
       </li>

       <li class="d-flex-history">
        <p>Supermercado</p>
        <p>R$ 300,00</p>
        <div class="flex items-cente q-gutter-sm">
          <q-btn color="red" size="sm" icon="delete"/>
          <q-btn color="orange" size="sm" icon="edit"/>
        </div>
       </li>

       <li class="d-flex-history">
        <p>Supermercado</p>
        <p>R$ 300,00</p>
        <div class="flex items-cente q-gutter-sm">
          <q-btn color="red" size="sm" icon="delete"/>
          <q-btn color="orange" size="sm" icon="edit"/>
        </div>
       </li>

       <li class="d-flex-history">
        <p>Supermercado</p>
        <p>R$ 300,00</p>
        <div class="flex items-cente q-gutter-sm">
          <q-btn color="red" size="sm" icon="delete"/>
          <q-btn color="orange" size="sm" icon="edit"/>
        </div>
       </li>


    </ul>
  </div>
</section>
 <footer>
    <div class="q-pa-lg flex flex-center">
      <q-pagination v-model="current" :max="5" />
    </div>
  </footer>
</template>

<script setup lang="ts">
import { ref } from "vue";
const current = ref(3)

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
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 35px;
  max-width:1024px;
  margin:0 auto;

  @media (max-width:868px){
    display:flex;
    flex-direction:column;
  }
}

.title-wallet{
  padding: 1rem 0;
}

.container-history{
  background-color: aliceblue;
  height: 440px;
  padding:10px;
}

.history{
    overflow-y: auto;
    height: 300px;
}

.d-flex-history{
  border-block:1px solid #ccc;
  display:grid;
  grid-template-columns: 1fr 1fr 1fr;
  align-items: center;
  padding:.6rem 0;

  @media (max-width:768px){
    display:flex;
    flex-direction:column;
    align-items: start;
    gap:15px;
    padding:1.2rem 0;
  }
}

.d-flex-history p{
  margin:0;
  padding:0;
}
</style>
