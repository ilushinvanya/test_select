<template lang="pug">
#app
	Select(:placeholder="'Сделай свой выбор'")
		template(v-slot:placeholder)
			span Custom placeholder

</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Select from './components/Select.vue';

@Component({
  components: {
    Select
  }
})
export default class App extends Vue {}
</script>

<style lang="stylus">
#app
  font-family Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  color #2c3e50
</style>
