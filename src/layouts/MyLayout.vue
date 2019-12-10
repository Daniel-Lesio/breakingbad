<template>
  <q-layout view="lHh Lpr lFf">
    <q-header id="head" class="row" >
      <q-toolbar class="col">
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          icon="menu"
          aria-label="Menu"
        />

        <q-toolbar-title  to="\">
          Breaking Bad
        </q-toolbar-title>
      </q-toolbar>
     <!-- <q-tabs class="flex">
          <q-route-tab to="/profile" replace icon="person" class="accent">

          </q-route-tab>
        </q-tabs> -->
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class=""
    >
      <q-list>
        
        <q-item clickable tag="a" target="_blank" href="https://github.com/Daniel-Lesio">
          <q-item-section avatar>
            <q-icon name="school" />
          </q-item-section>
          <q-item-section>
            <q-item-label>Autor</q-item-label>
            <q-item-label caption>numer 23</q-item-label>
          </q-item-section>
        </q-item>
        
        <q-separator />
        <q-item clickable tag="a" target="_blank" href='https://github.com/Daniel-Lesio'>
          <q-item-section avatar>
            <q-icon name="code" />
          </q-item-section>
          <q-item-section>
            <q-item-label>Github</q-item-label>
            <q-item-label caption>https://github.com/Daniel-Lesio</q-item-label>
          </q-item-section>
        </q-item>
       
       
       
        <q-separator />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
         <q-page-sticky position="bottom-right"  href="#head" :offset="[18, 18]">
            <q-btn v-on:click='test' fab icon="keyboard_arrow_up" color="primary" />
          </q-page-sticky>
    </q-page-container>
  </q-layout>
</template>

<script>
import { scroll } from 'quasar'
const { getScrollTarget, setScrollPosition } = scroll
export default {
  name: 'MyLayout',

  data () {
    return {
      leftDrawerOpen: false
    }
    
  },
  methods : {
     test(){
   
      const ele = document.getElementById('head') // You need to get your element here
      const target = getScrollTarget(ele)
      const offset = ele.offsetTop - ele.scrollHeight
      const duration =400
      setScrollPosition(target, offset, duration)
   
     } 
    }
}
</script>