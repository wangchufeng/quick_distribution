<template>
  <v-app>
    <v-app-bar app clipped-left color="rgba(141,215,255,1)" dense>
      <!-- <v-app-bar-nav-icon @click.stop="drawer = !drawer" /> -->
      <v-icon class="mx-4">fab fa-youtube</v-icon>
      <v-toolbar-title class="mr-12 align-center">
        <span class="title">website</span>
      </v-toolbar-title>
      <v-spacer />
      <v-row align="center" style="max-width: 650px">
        <v-text-field :append-icon-cb="() => {}" placeholder="Search..." single-line append-icon="search" color="white"
          hide-details />
      </v-row>
    </v-app-bar>

    <v-navigation-drawer :permanent="true" v-model="drawer" app clipped>
      <v-list dense>
        <v-list-item v-for="item in items" :key="item.text" link>
          <v-list-item-action>
            <v-icon>home</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>
              {{ item.text }}
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-content>
      <v-container>
        <canvas id="canvas"></canvas>
        <VueDragResize :isActive="true" :isResizable="false">
          <div class="d-flex justify-center">
            <v-color-picker></v-color-picker>
          </div>
        </VueDragResize>
      </v-container>
    </v-content>
    
  </v-app>
</template>

<script>
  import VueDragResize from 'vue-drag-resize'
  export default {
    components: {
      VueDragResize
    },
    data: () => ({
      drawer: null,
      items: [{
        icon: 'home',
        text: 'Most Popular'
      }, ],
    }),
    mounted() {
      this.initCanvas()
    },
    methods: {
      initCanvas() {
        let canvas = document.getElementById('canvas');
        
        let ctx = canvas.getContext('2d');
        let winW = window.innerWidth
        let winH = window.innerHeight
        canvas.width = winW
        canvas.height = winH
        this.drawSmile(ctx)
      },
      drawSmile(ctx) {
        ctx.beginPath();
        ctx.arc(75, 75, 50, 0, Math.PI * 2, true); // 绘制
        ctx.moveTo(110, 75);
        ctx.arc(75, 75, 35, 0, Math.PI, false); // 口(顺时针)
        ctx.moveTo(65, 65);
        ctx.arc(60, 65, 5, 0, Math.PI * 2, true); // 左眼
        ctx.moveTo(95, 65);
        ctx.arc(90, 65, 5, 0, Math.PI * 2, true); // 右眼
        ctx.stroke();
      }
    },
    created() {
      this.$vuetify.theme.dark = false
    },
  }
</script>