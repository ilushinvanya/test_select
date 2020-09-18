<template lang="pug">
	#app
		Select(
			v-model="select"
			:placeholder="'Сделай свой выбор'"
			:options="options_5"
			:disabled="false"
			:label_field="'title'"
			:value_field="'id'"
		)
			template(v-slot:placeholder)
				span Custom placeholder

		p {{ select }}
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import Select from './components/Select.vue';

    @Component({
        components: {
            Select
        },
        data() {
            return {
                select: false,
                options_1: ['Option1', 'Option2', 'Option3'],
				options_2: [
                    {
                        label: 'Preetish',
                        value: 1
                    },
                    {
                        label: 'John',
                        value: 2
                    },
                    {
                        label: 'Barbara',
                        value: 3
                    },
                    {
                        label: 'Gena',
                        value: 4
                    }
                ],
				options_3: [
				    { name: 'Option 1', id: 1},
					{ name: 'Option 2', id: 2 }
				],
				options_4: {
                    value1: 'Option 1',
					value2: 'Option 2'
				},
				options_5: {
                    value1: { title: 'Option 1', id: 1 },
					value2: { title: 'Option 2', id: 2 }
                }


        }
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
