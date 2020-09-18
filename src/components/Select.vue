<template lang="pug">
	div.select
		.select_container

			.select_container_input(
				@click="toogleOpen"
				:class="{disabled}")

				.select_value {{value_label}}

				.select_placeholder(v-if="!value")
					slot(name="placeholder") {{placeholder}}

			.select_clear(
				v-if="value"
				@click="clearInput")

		.select_options(:class="{hidden: !open, visible: open}")
			.option(
				v-for="option in options_parse"
				@click="changeOption(option.value)"
				@mouseover="focus_option = option.value"
				@mouseleave="focus_option = 0"
				:class="{focus: focus_option === option.value}"
			) {{option.label}}
</template>

<script lang="ts">
    import {Component, Prop, Vue} from 'vue-property-decorator';

    @Component
    export default class Select extends Vue {
        @Prop({default: 'placeholder'}) private placeholder!: string;
        @Prop({default: []}) private options!: Array<any>;
        @Prop({default: false}) private value!: any;
        @Prop({default: false}) private disabled!: boolean;
        @Prop({default: 'label'}) readonly label_field!: string;
        @Prop({default: 'value'}) readonly value_field!: string;

        private focus_option: number = 0;
        private open: boolean = false;

        private clearInput(): void {
            if (this.disabled) return
            this.open = false
            this.$emit("input", false)
        }

        private changeOption(option_value: any): void {
            this.$emit("input", option_value);
            this.toogleOpen()
        }

        private toogleOpen(): void {
            if (this.disabled) return;
            this.open = !this.open;
        }

        get value_label(): string {
            const find_of_option = this.options_parse.filter(option => option.value === this.value);

            if ( find_of_option !== undefined){
            	if ( Array.isArray(find_of_option) && find_of_option.length > 0){
					return find_of_option[0].label;
				}
			}
            return ""
        }

        get options_parse(): Array<object> {
            let result_options = [];

            const optionsIsArray = this.options instanceof Array;

            if ( typeof this.options === 'object' && !optionsIsArray ) {
                for (const [key, value] of Object.entries(this.options)) {

                    if ( typeof value === 'object' ){

                        result_options.push({
                            label: value[this.label_field],
                            value: value[this.value_field]
                        })

                    }else{

                        result_options.push({
                            label: value,
                            value: key
                        })

                    }
                }
            }

            if ( optionsIsArray ) {

                this.options.forEach(option => {
                    if (typeof option === 'string') {

                        result_options.push({
                            label: option,
                            value: option
                        })

                    } else if (typeof option === 'object') {

                        result_options.push({
                            label: option[this.label_field],
                            value: option[this.value_field]
                        })

                    }
                })
            }

            return result_options;
        }

    }
</script>

<style scoped lang="stylus">
	.select
		width 300px
		display block
		position relative

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
			width 18px
			height 18px
			cursor pointer
			opacity: 0.3;

			&:hover
				opacity 1

			&:before, &:after
				position absolute
				left 8px
				content ''
				height 100%
				width 2px
				background-color #333

			&:before
				transform rotate(45deg)

			&:after
				transform rotate(-45deg)

		&_options
			position absolute
			left 0
			top 100%
			background white
			z-index 3
			width 100%
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
