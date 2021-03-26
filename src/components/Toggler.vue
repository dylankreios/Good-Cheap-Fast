<template>
  <div class="toggler" :style="{ ...buttonSizeStyles }">
    <label>
      <input
        type="checkbox"
        :checked="checked"
        @input="$emit('updated', $event.target.checked)"
      />
      <span></span>
    </label>
    <strong>
      <slot />
    </strong>
  </div>
</template>

<script>
export default {
  props: ["size", "checked"],
  data() {
    return {
      buttonWidth: 50,
      buttonHeight: 30,
      toggleDiameter: 26,
      toggleWider: 34,
    };
  },
  computed: {
    buttonSizeStyles() {
      return {
        "--button-width": this.buttonWidth * this.size + "px",
        "--button-height": this.buttonHeight * this.size + "px",
        "--toggle-diameter": this.toggleDiameter * this.size + "px",
        "--toggle-wider": this.toggleWider * this.size + "px",
      };
    },
  },
};
</script>

<style scoped>
.toggler {
  --button-width: 500px;
  --button-height: 295px;
  --toggle-diameter: 255px;
  --toggle-wider: 333px;

  --button-toggle-offset: calc(
    (var(--button-height) - var(--toggle-diameter)) / 2
  );
  --toggle-shadow-offset: 10px;
  --color-gray: #e9e9ea;
  --color-dark-gray: #39393d;
  --color-green: #30d158;

  display: inline-flex;
}
.toggler strong {
  line-height: var(--button-height);
  font-size: var(--toggle-diameter);
  margin-left: calc(var(--toggle-diameter) / 4);
}
span {
  display: inline-block;
  width: var(--button-width);
  height: var(--button-height);
  background: var(--color-gray);
  border-radius: calc(var(--button-height) / 2);
  position: relative;
  transition: all 0.3s ease-in-out;
}
span::after {
  content: "";
  display: inline-block;
  position: absolute;
  width: var(--toggle-diameter);
  height: var(--toggle-diameter);
  background: #fff;
  border-radius: calc(var(--toggle-diameter) / 2);
  top: var(--button-toggle-offset);
  left: 0;
  transform: translateX(var(--button-toggle-offset));
  box-shadow: var(--toggle-shadow-offset) 0
    calc(var(--toggle-shadow-offset) * 4) rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease-in-out;
}
input[type="checkbox"] {
  display: none;
}
input[type="checkbox"]:checked + span {
  background: var(--color-green);
}
input[type="checkbox"]:checked + span::after {
  transform: translateX(
    calc(
      var(--button-width) - var(--toggle-diameter) - var(--button-toggle-offset)
    )
  );
  box-shadow: calc(var(--toggle-shadow-offset) * -1) 0
    calc(var(--toggle-shadow-offset) * 4) rgba(0, 0, 0, 0.1);
}
input[type="checkbox"]:active + span::after {
  width: var(--toggle-wider);
}
input[type="checkbox"]:checked:active + span::after {
  transform: translateX(
    calc(
      var(--button-width) - var(--toggle-wider) - var(--button-toggle-offset)
    )
  );
}
@media (prefers-color-scheme: dark) {
  body {
    background: #1c1c1e;
  }
  span {
    background: var(--color-dark-gray);
  }
}
</style>
