<template lang="pug">
	div.select
		.select_container(@click="toogleOpen")
			.select_input {{input}}
			.select_placeholder(v-if="!input") {{placeholder}}
		.select_options(:class="{hidden: !open, visible: open}")
			.option(v-for="option in list")(@click="changeOption(option.label)") {{option.label}}
</template>

<script lang="ts">
    import {Component, Prop, Vue} from 'vue-property-decorator';

    @Component
    export default class Select extends Vue {
        @Prop() private placeholder!: string;
        private input: string = "";
        private open: boolean = false;
        private list: Array<object> = [
            {
                label: 'Preetish',
                value: 1
            },
            {
                label: 'John',
                value: 2
            }
        ]

        public changeOption(option_name: string): void {
            // console.log(option)
            this.input = option_name;
            this.toogleOpen()
        }

        public toogleOpen(): void {
            this.open = !this.open;
        }


    }
</script>

<style scoped lang="stylus">
	.select
		width 300px
		display block

		&_container
			position relative
			border 1px blue solid
			border-radius 5px
			padding 10px

		&_options
			border 1px #c1c1c1 solid
			border-bottom 0

			&.hidden
				display none

			&.visible
				display block

			.option
				padding 10px
				border-bottom 1px #c1c1c1 solid
</style>
