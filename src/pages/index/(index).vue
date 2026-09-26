<template>
  <section class="page">
    <div class="navbar-search">
       <q-input placeholder="Buscar por..." outlined class="full-width"/>
      <q-btn label="cadastrar" icon="add" size="sm" color="green" @click="abrirModal" />
  </div>
    <q-dialog v-model="modal">
      <q-card class="card-modal">
        <div class="campos">
          <div class="header-form-register">
            <h1>Cadastro do cliente</h1>
            <q-btn @click="fecharModal" class="btn-close">
              <div class="btn-x">X</div>
              <div class="btn-label-cancelar">cancelar</div>
            </q-btn>
          </div>

          <q-input placeholder="Nome" outlined />
          <q-input placeholder="E-mail" outlined />
          <q-input placeholder="Telefone" outlined />
          <q-btn label="cadastrar" icon="add" size="sm" color="green" />
        </div>
      </q-card>
    </q-dialog>

 
    <div class="table-fake">
      <div class="row-fake">
        <h2>Lista de contatos</h2>
      </div>

      <div class="row-dados">
        <div>Carlos Nascimento</div>
        <div>carlosnas@mail.com</div>
        <div>88-9999-1010</div>
        <div class="flex q-gutter-md">
          <q-btn icon="delete"  size="sm" color="red" />
          <q-btn icon="edit" size="sm" color="orange" @click="abrirModal"/>
        </div>
      </div>


       <div class="row-dados">
        <div>Carlos Nascimento</div>
        <div>carlosnas@mail.com</div>
        <div>88-9999-1010</div>
        <div class="flex q-gutter-md">
          <q-btn icon="delete"  size="sm" color="red" />
          <q-btn icon="edit" size="sm" color="orange" @click="abrirModal"/>
        </div>
      </div>


       <div class="row-dados">
        <div>Carlos Nascimento</div>
        <div>carlosnas@mail.com</div>
        <div>88-9999-1010</div>
        <div class="flex q-gutter-md">
          <q-btn icon="delete"  size="sm" color="red" />
          <q-btn icon="edit" size="sm" color="orange" @click="abrirModal"/>
        </div>
      </div>


       <div class="row-dados">
        <div>Carlos Nascimento</div>
        <div>carlosnas@mail.com</div>
        <div>88-9999-1010</div>
        <div class="flex q-gutter-md">
          <q-btn icon="delete"  size="sm" color="red" />
          <q-btn icon="edit" size="sm" color="orange" @click="abrirModal"/>
        </div>
      </div>


      </div>
   </section>
  <footer>
    <div class="q-pa-lg flex flex-center">
      <q-pagination v-model="current" :max="5" />
    </div>
  </footer>
</template>

<script setup lang="ts">
import "@/css/formCadastro.scss";
import { ref } from "vue";
const current = ref(3)


const modal = ref(false);

function abrirModal(): void {
  modal.value = true;
}

function fecharModal(): void {
  modal.value = false;
}
</script>
