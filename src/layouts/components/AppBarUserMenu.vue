<template>
  <v-menu
    offset-y
    left
    nudge-bottom="14"
    min-width="230"
    content-class="user-profile-menu-content"
  >
    <template v-slot:activator="{ on, attrs }">
      <v-badge
        bottom
        color="success"
        overlap
        offset-x="12"
        offset-y="12"
        class="ms-4"
        dot
      >
        <v-avatar
          size="40px"
          v-bind="attrs"
          v-on="on"
        >
          <v-img :src="require('@/assets/images/logos/logoformunica.png')"></v-img>
        </v-avatar>
      </v-badge>
    </template>
    <v-list>
      <div class="pb-3 pt-2">
        <v-badge
          bottom
          color="success"
          overlap
          offset-x="12"
          offset-y="12"
          class="ms-4"
          dot
        >
          <v-avatar size="40px">
            <v-img :src="require('@/assets/images/avatars/1.png')"></v-img>
          </v-avatar>
        </v-badge>
        <div
          class="d-inline-flex flex-column justify-center ms-3"
          style="vertical-align:middle"
        >
          <span class="text--primary font-weight-semibold mb-n1">
            {{ usuario }}
          </span>
          <small class="text--disabled text-capitalize">{{ rol }}</small>
        </div>
      </div>

      <v-divider></v-divider>

      <!-- Profile -->
      <v-list-item link>
        <v-list-item-icon
          class="me-2"
          @click="perfil()"
        >
          <v-icon size="22">
            {{ icons.mdiAccountOutline }}
          </v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title @click="perfil()">
            Perfil
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider class="my-2"></v-divider>

      <!-- Settings -->
      <v-list-item
        v-if="rol == 110"
        link
      >
        <v-list-item-icon
          class="me-2"
          @click="config()"
        >
          <v-icon size="22">
            {{ icons.mdiCogOutline }}
          </v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title @click="config()">
            Configuración
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-divider
        v-if="rol == 110"
        class="my-2"
      ></v-divider>
      <!-- Logout -->
      <v-list-item link>
        <v-list-item-icon
          class="me-2"
          @click="cerrarSesion()"
        >
          <v-icon size="22">
            {{ icons.mdiLogoutVariant }}
          </v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title @click="cerrarSesion()">
            Cerrar Sesión
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-menu>
</template>

<script>
import {
  mdiAccountOutline,
  mdiEmailOutline,
  mdiCheckboxMarkedOutline,
  mdiChatOutline,
  mdiCogOutline,
  mdiCurrencyUsd,
  mdiHelpCircleOutline,
  mdiLogoutVariant,
} from '@mdi/js'

export default {
  setup() {
    return {
      icons: {
        mdiAccountOutline,
        mdiEmailOutline,
        mdiCheckboxMarkedOutline,
        mdiChatOutline,
        mdiCogOutline,
        mdiCurrencyUsd,
        mdiHelpCircleOutline,
        mdiLogoutVariant,
      },
    }
  },
  data: () => ({
    usuario: '',
    rol: '',
  }),
  created() {
    this.usuario = sessionStorage.getItem('user')
    this.rol = sessionStorage.getItem('roleFormunica')
  },
  methods: {
    cerrarSesion() {
      sessionStorage.removeItem('tknHonduras')
      sessionStorage.removeItem('user')
      sessionStorage.removeItem('roleFormunica')
      sessionStorage.removeItem('cod_vend')
      this.$router.push({ name: 'pages-login' })
    },
    perfil() {
      this.$router.push({ name: 'pages-account-settings' })
    },
    config() {
      this.$router.push({ name: 'pages-configuration' })
    },
  },
}
</script>

<style lang="scss">
.user-profile-menu-content {
  .v-list-item {
    min-height: 2.5rem !important;
  }
}
</style>
