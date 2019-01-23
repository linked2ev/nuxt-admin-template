<template>
<div>
  <v-toolbar
    :clipped-left="$vuetify.breakpoint.lgAndUp"
    color="blue darken-3"
    dark
    app
    fixed
    height="35"
  >
    <!-- header -->
    <v-toolbar-title style="width: 300px" class="ml-0 pl-3">
    <v-toolbar-side-icon @click.stop="fnDrawer"></v-toolbar-side-icon>
    <span class="hidden-sm-and-down" v-text="appName"></span>
    </v-toolbar-title>

    <v-spacer></v-spacer>
    <span>
      {{ $store.state.authUser }}
    </span>
    <v-btn icon>
      <v-icon>apps</v-icon>
    </v-btn>
    <v-btn icon @click.prevent="fnLogout">
      <v-icon>logout</v-icon>
    </v-btn>
    <v-btn icon @click.stop="fnRightDrawer">
      <v-icon light>compare_arrows</v-icon>
    </v-btn>
    <!-- //header -->

    <!-- header Tab -->
    <v-tabs
        slot="extension"
        color="blue darken-3"
        slider-color="yellow"
        height="35"
        grow
      >
        <v-tab
          v-for="menu in $store.state.topMenu"
          :key="menu.id"
        >
          {{menu.NAME}}
        </v-tab>
      </v-tabs>
    <!-- //header Tab -->
  </v-toolbar>
</div>
</template>

<script>
export default {
  props: ['appName', 'drawer', 'rightDrawer'],
  data: () => ({
    drawerChild: null,
    rightDrawerChild: null
  }),
  methods: {
    fnDrawer () {
      this.drawerChild = this.drawerChild === true ? false : true;
      this.$emit('isDrawer', this.drawerChild);
    },
    fnRightDrawer () {
      this.rightDrawerChild = this.rightDrawerChild === true ? false : true;
      this.$emit('isRightDrawer', this.rightDrawerChild);
    },
    fnLogout () {
      this.$store.dispatch('logout').then(() => this.$router.push('/v1/login'))
    }
  },
  watch: {
    drawer (value) {
      this.drawerChild = value;
    },
    rightDrawer (value) {
      this.rightDrawerChild = value;
    }
  }
}
</script>