<script>
	// PROPS

	// Common & Required
	export let title = 'Checkbox'
	export let checked = false
	export let disabled = false
	export let onChange = () => {}
	export let size = 'sm' || 'md' || 'lg'

	// Customzation
	export let inactiveTrackFillColor = '#ffffff'
	export let inactiveTrackStrokeColor = '#d1d1d1'
	export let activeTrackFillColor = '#ff708f'
	export let activeTrackStrokeColor = '#ff4e74'
	export let disabledTrackFillColor = '#f2f2f2'
	export let disabledTrackStrokeColor = '#d1d1d1'
	export let invalidTrackFillColor = '#ffffff'
	export let invalidTrackStrokeColor = '#d1d1d1'
	export let inactiveThumbColor = '#ffffff'
	export let activeThumbColor = '#ffffff'
	export let disabledThumbColor = '#ffffff'
	export let invalidThumbColor = '#ffffff'
	export let thumbShadowColor = 'rgb(23 23 23 / 0.25)'
	export let thumbFocusRingColor = 'rgb(59 130 246 / 0.5)'
	export let animationDuration = 350

	// FUNCTIONS
	function sizeToScale() {
		switch (size) {
			case 'sm':
				return 1
			case 'md':
				return 1.5
			case 'lg':
				return 2
		}
	}

	function handleOnChange() { 
		initialState = false
		onChange()
	}

	// VARIABLES
	const initialChecked = checked
	let initialState = true
	let scale = sizeToScale() || 1

	// $: console.log(`initialState = ${initialState}`)
	// $: console.log(`initialChecked = ${initialChecked}`)
	// $: console.log(`checked = ${checked}`)

</script>

<span
	style="
    --inactiveTrackFillColor: {inactiveTrackFillColor};
    --inactiveTrackStrokeColor: {inactiveTrackStrokeColor};
    --activeTrackFillColor: {activeTrackFillColor};
    --activeTrackStrokeColor: {activeTrackStrokeColor};
    --disabledTrackFillColor: {disabledTrackFillColor};
    --disabledTrackStrokeColor: {disabledTrackStrokeColor};
    --invalidTrackFillColor: {invalidTrackFillColor};
    --invalidTrackStrokeColor: {invalidTrackStrokeColor};
    --inactiveThumbColor: {inactiveThumbColor};
    --activeThumbColor: {activeThumbColor};
    --disabledThumbColor: {disabledThumbColor};
    --invalidThumbColor: {invalidThumbColor};
    --thumbShadowColor: {thumbShadowColor};
    --thumbFocusRingColor: {thumbFocusRingColor};
    --scale: {scale};
    --animationDuration: {animationDuration}ms;
    "
>
	<label
		class:disabled
		class:checked
		class:initialState
	>
		<input type="checkbox" role="switch" bind:checked {disabled} on:change={() => handleOnChange()} />
		<svg
			xmlns="http://www.w3.org/2000/svg"
			viewBox="0 0 33 23"
			aria-hidden="true"
		>
			<path
				d="M23.5,0.5 C28.4705627,0.5 32.5,4.52943725 32.5,9.5 C32.5,16.9484448 21.46672,22.5 16.5,22.5 C11.53328,22.5 0.5,16.9484448 0.5,9.5 C0.5,4.52952206 4.52943725,0.5 9.5,0.5 C12.3277083,0.5 14.8508336,1.80407476 16.5007741,3.84362242 C18.1491664,1.80407476 20.6722917,0.5 23.5,0.5 Z"
			/>
		</svg>
	</label>
</span>

<style>
	@keyframes check {
		0% {
			transform: rotate(30deg);
		}

		25% {
			transform: rotate(30deg) translateX(calc(4.5px * var(--scale)))
				scaleX(1.1);
		}

		50% {
			transform: rotate(30deg) translateX(calc(9px * var(--scale)));
		}

		100% {
			transform: rotate(-30deg) translateX(calc(13.5px * var(--scale)))
				translateY(calc(8px * var(--scale)));
		}
	}

	@keyframes uncheck {
		0% {
			transform: rotate(-30deg) translateX(calc(13.5px * var(--scale)))
				translateY(calc(8px * var(--scale)));
		}

		50% {
			transform: rotate(30deg) translateX(calc(9px * var(--scale)));
		}

		75% {
			transform: rotate(30deg) translateX(calc(4.5px * var(--scale)))
				scaleX(1.1);
		}

		100% {
			transform: rotate(30deg);
		}
	}

	label {
		position: relative;
		display: block;
		cursor: pointer;
		-webkit-tap-highlight-color: transparent;
	}

	input {
		position: absolute;
		top: calc(1px * var(--scale));
		left: calc(1px * var(--scale));
		transition: border-width 50ms background-color var(--animationDuration);
		appearance: none;
		margin: 0;
		box-shadow: 0 0 calc(2px * var(--scale)) calc(1px * var(--scale))
			var(--thumbShadowColor);
		outline: none;
		border: 0 solid var(--thumbFocusRingColor);
		border-radius: 50%;
		width: calc(18px * var(--scale));
		height: calc(18px * var(--scale));
		background-color: var(--inactiveThumbColor);
		pointer-events: none;
		animation-duration: var(--animationDuration);
	}

	input + svg {
		display: block;
		transition: fill var(--animationDuration),
			stroke var(--animationDuration);
		width: calc(36px * var(--scale));
		height: calc(25px * var(--scale));
		fill: var(--inactiveTrackFillColor);
		stroke: var(--inactiveTrackStrokeColor);
		stroke-linejoin: round;
		border-width: calc(1px * var(--scale));
	}

	input:checked {
		animation-name: check;
		animation-timing-function: linear;
		animation-fill-mode: forwards;
		background-color: var(--activeThumbColor);
	}

	input:checked + svg {
		fill: var(--activeTrackFillColor);
		stroke: var(--activeTrackStrokeColor);
	}

	input:not(:checked) {
		animation-name: uncheck;
		animation-timing-function: linear;
		animation-fill-mode: backwards;
	}

	input:focus {
		border-width: calc(1px * var(--scale));
	}

	input:focus:not(:focus-visible) {
		border-width: 0;
	}

	input:focus-visible {
		border-width: calc(1px * var(--scale));
	}

	input:invalid {
		background-color: var(--invalidThumbColor);
	}

	label.initialState > input, .initialState > svg {
		animation-duration: 0ms !important;
	}
</style>
