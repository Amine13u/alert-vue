<template>
  <div class="alert" :class="alertClasses" v-show="show">
    <div class="alert-icon">
      <component :is="alertIcon"></component>
    </div>
    <div class="alert-content">
      <div class="alert-title">{{ alertTitle }}</div>
      <div class="alert-msg">{{ msg }}</div>
    </div>
    <button class="alert-btn" @click="$emit('hide')">&times;</button>
  </div>
</template>

<script>
import IconError from "./IconError.vue";
import IconWarning from "./IconWarning.vue";
import IconSuccess from "./IconSuccess.vue";
export default {
  emits: ["hide"],
  data: () => ({
    timer: null,
  }),
  watch: {
    show() {
      if (this.timer) {
        clearTimeout(this.timer);
      }
      this.timer = setTimeout(() => {
        this.$emit("hide");
      }, 5000);
    },
  },
  props: {
    title: {
      type: String,
      default: null,
    },
    msg: {
      type: String,
      required: true,
    },
    show: {
      type: Boolean,
      default: false,
    },
    type: {
      type: String,
      default: "success",
      validator: function (value) {
        return ["success", "warning", "error"].indexOf(value) !== -1;
      },
    },
    position: {
      type: String,
      default: "bottom-right",
    },
  },
  computed: {
    alertType() {
      return `alert-${this.getType}`;
    },
    alertIcon() {
      return `icon-${this.getType}`;
    },
    getType() {
      return ["success", "warning", "error"].indexOf(this.type) === -1
        ? "success"
        : this.type;
    },
    alertTitle() {
      return this.title
        ? this.title.charAt(0).toUpperCase() + this.title.slice(1)
        : this.type.charAt(0).toUpperCase() + this.type.slice(1);
    },
    getPosition() {
      return ["bottom-left", "bottom-right", "top-left", "top-right"].indexOf(
        this.position
      ) === -1
        ? "bottom-right"
        : this.position;
    },
    alertClasses() {
      return [this.alertType, this.getPosition];
    },
  },
  components: {
    IconError,
    IconWarning,
    IconSuccess,
  },
};
</script>

<style scoped>
.alert {
  width: 300px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  box-shadow: 1px 5px 10px -5px rgba(0, 0, 0, 0.5);
  border-radius: 5px;
}

.alert-icon {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  padding: 7px;
}

.alert-success .alert-icon svg {
  fill: lightgreen;
}

.alert-success {
  background: lightgreen;
}

.alert-success .alert-icon {
  background-color: rgb(7, 167, 7);
}

.alert-warning .alert-icon svg {
  fill: lightyellow;
}

.alert-warning {
  background: lightyellow;
}

.alert-warning .alert-icon {
  background-color: rgb(250, 250, 50);
}

.alert-error .alert-icon svg {
  fill: lightcoral;
}

.alert-error {
  background: lightcoral;
}

.alert-error .alert-icon {
  background-color: rgb(215, 5, 5);
}

.alert-content {
  flex-grow: 1;
  margin: 0 1rem;
}

.alert-title {
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.alert-msg {
  font-size: 15px;
  color: rgb(100, 100, 100);
}

.alert-btn {
  width: 1.5em;
  height: 1.5em;
  border: none;
  padding: 0;
  background: transparent;
  color: rgb(100, 100, 100);
  cursor: pointer;
  font-size: 1.5em;
  opacity: 0.7;
}

.alert-btn:hover {
  opacity: 1;
}

.bottom-left {
  position: fixed;
  left: 20px;
  bottom: 20px;
}
.top-left {
  position: fixed;
  left: 20px;
  top: 20px;
}
.bottom-right {
  position: fixed;
  right: 20px;
  bottom: 20px;
}
.top-right {
  position: fixed;
  right: 20px;
  top: 20px;
}
</style>
