<template>
<div>
  <v-navigation-drawer
    :clipped="$vuetify.breakpoint.lgAndUp"
    v-model="drawerChild"
    fixed
    app
  >
    <v-list dense>
      <template v-for="item in items">
        <v-layout
          v-if="item.heading"
          :key="item.heading"
          row
          align-center
        >
          <v-flex xs6>
            <v-subheader v-if="item.heading">
              {{ item.heading }}
            </v-subheader>
          </v-flex>
          <v-flex xs6 class="text-xs-center">
            <a href="#!" class="body-2 black--text">EDIT</a>
          </v-flex>
        </v-layout>

        <v-list-group
          v-else-if="item.children"
          v-model="item.model"
          :key="item.text"
          :prepend-icon="item.model ? item.icon : item['icon-alt']"
          append-icon=""
        >
          <!-- 1 depth Group Btn -->
          <v-list-tile slot="activator">
            <v-list-tile-content>
              <v-list-tile-title>
                {{ item.text }}
              </v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <!-- //1 depth Group Btn -->

          <!-- 2 depth Group Btn -->
          <v-list-tile
            v-for="(child, i) in item.children"
            :key="i"
          >
            <v-list-tile-action v-if="child.icon">
              <v-icon>{{ child.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>
                {{ child.text }}
              </v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <!-- //2 depth Group Btn -->
        </v-list-group>

        <!-- 1 depth Btn -->
        <v-list-tile v-else :key="item.text" :to="item.to">
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>
              {{ item.text }}
            </v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <!-- //1 depth Btn -->

      </template>
    </v-list>
  </v-navigation-drawer>
</div>
</template>

<script>
export default {
  props: ['drawer'],
  data: () => ({
    drawerChild: null,
    //itemList: []
    items: [
      { icon: 'contacts', text: 'Index', to: '/' },
      { icon: 'history', text: 'Inspire', to: '/Inspire' },
      { icon: 'content_copy', text: '메뉴 1', to: '/about' },
      {
        icon: 'keyboard_arrow_up',
        'icon-alt': 'keyboard_arrow_down',
        text: '메뉴 2',
        model: false,
        children: [
          { icon: 'add', text: '메뉴 2-1' }
        ]
      },
      {
        icon: 'keyboard_arrow_up',
        'icon-alt': 'keyboard_arrow_down',
        text: '메뉴 3',
        model: false,
        children: [
          { text: '메뉴 3-1' },
          { text: '메뉴 3-2' },
          { text: '메뉴 3-3' },
          { text: '메뉴 3-4' },
          { text: '메뉴 3-5' }
        ]
      },
      { icon: 'settings', text: '메뉴 4' },
      { icon: 'chat_bubble', text: '메뉴 5' },
      { icon: 'help', text: '메뉴 6' },
      { icon: 'phonelink', text: '메뉴 7' }
    ]
  }),
  watch: {
    drawer (value) {
      this.drawerChild = value;
    },
    drawerChild (value) {
      this.$emit('isDrawer', value)
    }
  }
}
</script>