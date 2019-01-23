<template>
<div>
  <v-navigation-drawer
    temporary
    :right="right"
    v-model="rightDrawerChild"
    :width="350"
    fixed
  >
    <v-list>
      <v-list-tile>
        <v-list-tile-action>
          <v-icon light>keyboard</v-icon>
        </v-list-tile-action>
        <v-list-tile-title>Chatflow</v-list-tile-title>
      </v-list-tile>
    </v-list>

  </v-navigation-drawer>
</div>
</template>

<script>
export default {
  props: ['rightDrawer'],
  data: () => ({
    right: true,
    rightDrawerChild: null
  }),
  watch: {
    rightDrawer (value) {
      this.rightDrawerChild = value;
    },
    rightDrawerChild (value) {
      this.$emit('isRightDrawer', value)
    }
  }
}
</script>