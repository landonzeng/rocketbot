<template>
  <header class="rk-header">
    <div class="rk-header-start">
      <img class="mr10" :src="require('@/assets/img/logo.svg')"/>
      <span class="logo">Rocketbot</span>
    </div>
    <nav class="rk-nav">
      <router-link class="rk-nav-link" to="/" exact>Dashboard</router-link>
      <router-link class="rk-nav-link" to="/topo">Topology</router-link>
      <router-link class="rk-nav-link" to="/trace">Trace</router-link>
      <router-link class="rk-nav-link" to="/alarm">Alarm</router-link>
    </nav>
    <div class="rk-header-end">
      <div v-clickout="() => this.show = false">
        <div class="flex-c cp" @click="show = !show;">
          <span class="mr5 sm">{{time.start | dateformat}} ~ {{time.end | dateformat}}</span>
          <ion-icon :name="show?'arrow-dropup':'arrow-dropdown'" size="small" class="mr10"></ion-icon>
        </div>
        <RkToolTime :show.sync="show" :propsTime="time"/>
      </div>
      <div class="rk-nav-auto cp flex-c" @click="$store.dispatch('RUN_EVENTS')"><ion-icon name="refresh" class="mr5"></ion-icon>reload</div>
    </div>
  </header>
</template>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';
import RkToolTime from '@/components/rk-tool-time.vue';

@Component({
  components: { RkToolTime },
})
export default class Header extends Vue {
  show = false;
  @Prop() time: any;
}
</script>

<style lang="scss" scoped>
.rk-header {
  flex-shrink: 0;
  z-index: 10;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 30px;
  background-color: #252a2f;
  color: #eaeaea;
  width: 100%;
  box-shadow: 0 1px 2px 0 rgba(0,0,0,.06);
  .logo{
     font-family: 'Avenir', Helvetica, Arial, sans-serif;
     font-size: 18px;
     padding-top: 2px;
  }
}
.rk-header-start,.rk-header-end{
  display: flex;
  align-items: center;
}
.rk-nav-link{
  margin-right: 20px;
  padding: 6px 10px;
  border-radius: 6px;
  color: #eaeaea;
  opacity: .8;
  will-change: opacity, background-color;
  transition: opacity .3s, background-color .3s;
  &:hover,&.active{
    opacity: 1;
    background-color: rgba(255,255,255,.07);
    box-shadow: 0 3px 6px 0 rgba(0,0,0,.1), 0 1px 3px 0 rgba(0,0,0,.08);
  }
}
.rk-nav-auto{
  border-radius: 4px;
  padding: 1px 6px;
  background-color: rgba(255,255,255,.07);
  box-shadow: 0 3px 6px 0 rgba(0,0,0,.1), 0 1px 3px 0 rgba(0,0,0,.08);
}
</style>
