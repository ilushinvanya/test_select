<template lang="pug">
	div.select
		.select_container

			.select_container_input(
				@click="toogleOpen"
				:class="{disabled}")

				.select_value {{input}}
				.select_placeholder(v-if="!input")
					slot(name="placeholder") {{placeholder}}

			.select_clear(
				v-if="input"
				@click="clearInput")

		.select_options(:class="{hidden: !open, visible: open}")
			.option(
				v-for="option in list"
				@click="changeOption(option.label)"
				@mouseover="focus_option = option.value"
				@mouseleave="focus_option = 0"
				:class="{focus: focus_option === option.value}"
				) {{option.label}}
</template>

<script lang="ts">
    import {Component, Prop, Vue} from 'vue-property-decorator';

    @Component
    export default class Select extends Vue {
        @Prop() private placeholder!: string;
        private input: string = "input";
        private focus_option: number = 0;
        private disabled: boolean = false;
        private open: boolean = false;
        private list: Array<object> = [
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
        ]

        public clearInput(): void {
            if (this.disabled) return;
            this.input = ""
		}
        public changeOption(option_name: string): void {
            this.input = option_name;
            // this.$emit("input", option)
            this.toogleOpen()
        }

        public toogleOpen(): void {
            if (this.disabled) return;
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
			overflow hidden
			&_input
				padding 10px
				&.disabled:before
					content ""
					position absolute
					z-index 2
					width 100%
					height 100%
					top 0
					left 0
					background rgba(255, 255, 255, 0.7)
		&_clear
			position absolute
			right 7px
			top 50%
			transform translateY(-50%)
			background #adadad
			width 18px
			height 18px
			cursor pointer
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
				&.focus
					background #dddae2
</style>
