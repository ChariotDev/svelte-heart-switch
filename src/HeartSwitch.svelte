<script>
	export let size = 'small' || 'medium' || 'large'
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
	const TOGGLE_ANIMATION_DURATION = 350
	export let title

	function sizeToScale() {
		switch (size) {
			case 'small':
				return 1
			case 'medium':
				return 1.5
			case 'large':
				return 2
		}
	}

    let  scale = sizeToScale()
	let disabled = false
	let checked = false
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
    --TOGGLE_ANIMATION_DURATION: {TOGGLE_ANIMATION_DURATION};
    "
>
	<label class:disabled class:checked on:click|preventDefault={() => checked = !checked} >
		<input type="checkbox" role="switch" checked={checked} />
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
			transform: rotate(30deg) translateX(calc(9 * var(--scale)) px);
		}

		100% {
			transform: rotate(-30deg) translateX(calc(13.5px * var(--scale)))
				translateY(calc(8px * var(--scale)));
		}
	}

	@keyframes unckeck {
		0% {
			transform: rotate(-30deg)
				translateX(
					calc(13.5px * var(--scale))
						translateY(calc(8px * var(--scale)))
				);
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
		top: calc(1px * var(--size));
		left: calc(1px * var(--size));
		transition: border-width 50ms background-color 350ms;
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
	}

	svg {
		display: block;
		transition: fill var(--TOGGLE_ANIMATION_DURATION)ms,
			stroke var(--TOGGLE_ANIMATION_DURATION)ms;
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

	input:not(:checked) {
		animation-name: uncheck;
		animation-timing-function: linear;
		animation-fill-mode: backwards;
	}

	svg:focus {
		border-width: calc(1px * var(--scale));
	}

	svg:focus:not(:focus-visible) {
		border-width: 0;
	}

	svg:focus-visible {
		border-width: calc(1px * var(--scale));
	}

	svg:invalid {
		background-color: var(--invalidThumbColor);
	}
</style>
