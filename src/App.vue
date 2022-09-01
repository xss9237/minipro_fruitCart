<template>
    <div>
        <fruit-list></fruit-list>
    </div>
</template>

<script>
// import MyHeader from './components/my-header/MyHeader.vue'
// import FruitList from './components/fruit-list/FruitList.vue'
import FruitList from './components/01fruit-list/FruitList.vue'

export default {
  name: 'MyApp',
  components: {
    // MyHeader,
    FruitList
  }
}
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
}
</style>
