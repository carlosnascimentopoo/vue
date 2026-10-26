<template>
  <section class="page">
    <div class="navbar-search">
      <q-input placeholder="Buscar por..." outlined class="full-width" />
      <q-btn
        label="cadastrar"
        icon="add"
        size="sm"
        color="green"
        @click="abrirModalNovo"
      />
    </div>

    <q-dialog v-model="modal">
      <q-card class="card-modal">
        <div class="campos">
          <div class="header-form-register">
            <h1>{{ editando ? 'Editar cliente' : 'Cadastro do cliente' }}</h1>
            <q-btn @click="fecharModal" class="btn-close">
              <div class="btn-x">X</div>
              <div class="btn-label-cancelar">cancelar</div>
            </q-btn>
          </div>

          <q-input placeholder="Nome completo" outlined v-model="formulario.nome" />
          <q-input placeholder="E-mail" outlined v-model="formulario.email" />
          <q-input placeholder="Telefone" outlined v-model="formulario.telefone" />

          <q-btn
            :label="editando ? 'Salvar' : 'Cadastrar'"
            icon="add"
            size="sm"
            color="green"
            @click="cadastrarOuEditar"
          />
        </div>
      </q-card>
    </q-dialog>

    <div class="table-fake">
      <div class="row-fake">
        <h2>Lista de contatos</h2>
      </div>

      <div class="row-dados" v-for="usuario in usuarios" :key="usuario.id">
        <div>{{ usuario.nome }}</div>
        <div>{{ usuario.email }}</div>
        <div>{{ usuario.telefone }}</div>
        <div class="flex q-gutter-md">
          <q-btn icon="delete" size="sm" color="red" @click="removerUsuario(usuario.id)" />
          <q-btn icon="edit" size="sm" color="orange" @click="abrirModalEditar(usuario)" />
        </div>
      </div>
    </div>
  </section>
  <footer>
    <div class="q-pa-lg flex flex-center">
      <q-pagination :max="5" />
    </div>
  </footer>
</template>

<script setup lang="ts">
import "@/css/formCadastro.scss";
import { useQuasar } from "quasar";
import { ref } from "vue";

interface Formulario {
  nome: string;
  email: string;
  telefone: string;
}

interface Usuario extends Formulario {
  id: number;
}

const $q = useQuasar();

const formulario = ref<Formulario>({
  nome: "",
  email: "",
  telefone: "",
});

const usuarios = ref<Usuario[]>([
  {
    id: 1,
    nome: "carla",
    email: "carlos@gail.com",
    telefone: "889999-1111",
  },
  {
    id: 2,
    nome: "jose",
    email: "jose@gail.com",
    telefone: "889999-1111",
  },
]);

const modal = ref(false);
const editando = ref(false);
const usuarioEmEdicao = ref<Usuario | null>(null);

// ─────────── MODAL ───────────
function abrirModalNovo() {
  formulario.value = { nome: "", email: "", telefone: "" };
  editando.value = false;
  usuarioEmEdicao.value = null;
  modal.value = true;
}

function abrirModalEditar(usuario: Usuario) {
  formulario.value = { ...usuario };
  editando.value = true;
  usuarioEmEdicao.value = usuario;
  modal.value = true;
}

function fecharModal() {
  modal.value = false;
}

// ─────────── CADASTRAR / EDITAR ───────────
function cadastrarOuEditar() {
  const { nome, email, telefone } = formulario.value;

  // 1. Campos preenchidos
  if (!nome.trim()) {
    $q.dialog({
      title: "Atenção",
      message: "Por favor, preencha o campo NOME.",
      ok: { label: "Entendi", color: "primary" },
    });
    return;
  }
  if (!email.trim()) {
    $q.dialog({
      title: "Atenção",
      message: "Por favor, preencha o campo E-MAIL.",
      ok: { label: "Entendi", color: "primary" },
    });
    return;
  }
  if (!telefone.trim()) {
    $q.dialog({
      title: "Atenção",
      message: "Por favor, preencha o campo TELEFONE.",
      ok: { label: "Entendi", color: "primary" },
    });
    return;
  }

  // 2. Mais de 10 caracteres
  if (nome.trim().length <= 10) {
    $q.dialog({
      title: "Atenção",
      message: "O NOME deve ter mais de 10 caracteres.",
      ok: { label: "Entendi", color: "primary" },
    });
    return;
  }
  if (email.trim().length <= 10) {
    $q.dialog({
      title: "Atenção",
      message: "O E-MAIL deve ter mais de 10 caracteres.",
      ok: { label: "Entendi", color: "primary" },
    });
    return;
  }
  if (telefone.trim().length <= 10) {
    $q.dialog({
      title: "Atenção",
      message: "O TELEFONE deve ter mais de 10 caracteres.",
      ok: { label: "Entendi", color: "primary" },
    });
    return;
  }

  // 3. E-mail válido
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(email.trim())) {
    $q.dialog({
      title: "Atenção",
      message: "Por favor, informe um E-MAIL válido.",
      ok: { label: "Entendi", color: "primary" },
    });
    return;
  }

  // ── TUDO OK ──
  if (editando.value && usuarioEmEdicao.value) {
    // Atualizar
    const idx = usuarios.value.findIndex((u) => u.id === usuarioEmEdicao.value!.id);
    if (idx !== -1) {
      usuarios.value[idx] = {
        ...usuarios.value[idx],
        ...formulario.value,
      };
      $q.notify({
        message: "Cliente atualizado com sucesso!",
        color: "green",
        icon: "check",
      });
    }
  } else {
    // Cadastrar (ID sequencial seguro)
    const maiorId = usuarios.value.length > 0
      ? Math.max(...usuarios.value.map((u) => u.id))
      : 0;
    const novoId = maiorId + 1;

    usuarios.value.push({
      ...formulario.value,
      id: novoId,
    });

    $q.notify({
      message: "Cliente cadastrado com sucesso!",
      color: "green",
      icon: "check",
    });
  }
  fecharModal();
}

// ─────────── REMOVER ───────────
function removerUsuario(id: number) {
  $q.dialog({
    title: "Confirmação",
    message: "Deseja excluir este cliente?",
    cancel: { label: "Cancelar", color: "grey" },
    ok: { label: "Excluir", color: "red" },
  }).onOk(() => {
    usuarios.value = usuarios.value.filter((u) => u.id !== id);
    $q.notify({
      message: "Cliente excluído.",
      color: "red",
      icon: "delete",
    });
  });
}
</script>
