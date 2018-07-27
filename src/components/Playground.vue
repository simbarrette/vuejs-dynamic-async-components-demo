<template>
  <section class="playground">
    <h1>Welcome to the component playground!</h1>
    <button v-on:click="addActiveComponent">Add a new component</button>
    <hr>
    <div class="test" v-for="(item, index) in activeComponents" :key="index">
      <keep-alive>
        <component :is="item.component"></component>
      </keep-alive>
    </div>
  </section>
</template>

<script>
import Button from '@/components/dynamic/Button'
import Header from '@/components/dynamic/Header'
// Comment out the line below, since we will be loading it asynchronously
// import TextInput from '@/components/dynamic/TextInput'

export default {
  name: 'Playground',
  data: function () {
    return {
      componentList: [
        { label: 'Button', component: Button },
        { label: 'Header', component: Header },
        {
          label: 'TextInput',
          // Async loading!
          component: () => import('@/components/dynamic/TextInput')
        }
      ],
      numberOfComponents: 0,
      activeComponents: []
    }
  },

  methods: {
    addActiveComponent: function (event) {
      if (event) {
        if (this.numberOfComponents < this.componentList.length) {
          this.activeComponents.push(this.componentList[this.numberOfComponents])
          this.numberOfComponents += 1
          console.log('Component added')
        }
      }
    }
  }
}
</script>
