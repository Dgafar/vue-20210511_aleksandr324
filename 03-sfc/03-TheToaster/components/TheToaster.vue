<template>
  <div class="toasts">
    <one-event v-for="toast in toasts" :key="toast.id" :class-toast="toast.classToast" :icon-toast="toast.iconToast" :message="toast.message">
    </one-event>
  </div>
</template>

<script>
import OneEvent from "./OneEvent";

const DELAY = 5000;

export default {
  name: "TheToaster",

  components: { OneEvent },

  data() {
    return {
      toasts: []
    };
  },

  methods: {
    error(message) {
      this.toasts.push({message, classToast: 'toast_error', iconToast: 'alert-circle'});
      this.toastSplice();
    },
    success(message) {
      this.toasts.push({message, classToast: 'toast_success', iconToast: 'check-circle'});
      this.toastSplice();

    },

    toastSplice() {
        window.setInterval(() => {
          this.toasts.splice(0, 1);
        }, DELAY)
    }
  }
};
</script>

<style scoped>
.toasts {
  position: fixed;
  bottom: 8px;
  right: 8px;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  white-space: pre-wrap;
  z-index: 999;
}

.toast {
  display: flex;
  flex: 0 0 auto;
  flex-direction: row;
  align-items: center;
  padding: 16px;
  background: #ffffff;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
  border-radius: 4px;
  font-size: 18px;
  line-height: 28px;
  width: auto;
}

.toast + .toast {
  margin-top: 20px;
}

.toast > .icon {
  margin-right: 12px;
}

.toast.toast_success {
  color: var(--green);
}

.toast.toast_error {
  color: var(--red);
}

@media all and (min-width: 992px) {
  .toasts {
    bottom: 72px;
    right: 112px;
  }
}
</style>
