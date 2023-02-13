<script setup>
/**
 * Requirments:
 * - intent: success, warning, danger, info
 * - icon base on intent: checkmark, triangle, x, info
 * - title & content
 * - dismissable
 *
 * Pengelompokan:
 * Setelah kelas dipisah, kita dapat 'mengelompokkannya' agar lebih rapi dan mudah dibaca.
 * Pola yang biasa saya terapkan adalah:
 * - group 1: utilitas bawaan
 * - group 2: utilitas breakpoint
 * - group 3: utilitas mode gelap
 * - group 4: utilitas varian lain
 */

import {
  InformationCircleIcon,
  CheckCircleIcon,
  ExclamationTriangleIcon,
  XCircleIcon,
  XMarkIcon,
} from "@heroicons/vue/20/solid/index.js";
import { computed } from "vue";
import { cva } from "class-variance-authority";

const containerClass = computed(() => {
  return cva("flex p-4 rounded-lg space-x-3 md:rounded-xl dark:bg-gray-800", {
    variants: {
      intent: {
        info: "bg-blue-100",
        success: "bg-green-100",
        warning: "bg-orange-100",
        danger: "bg-red-100",
      },
    },
  })({
    intent: props.intent,
  });
});
const iconClass = computed(() => {
  return cva("w-6 h-6", {
    variants: {
      intent: {
        info: "text-blue-700 dark:text-blue-400",
        success: "text-green-500 dark:text-green-400",
        warning: "text-orange-400 dark:text-orange-400",
        danger: "text-red-600 dark:text-red-400",
      },
    },
  })({
    intent: props.intent,
  });
});
const titleClass = computed(() => {
  return cva("font-medium", {
    variants: {
      intent: {
        info: "text-blue-900 dark:text-blue-500",
        success: "text-green-900 dark:text-green-500",
        warning: "text-orange-900 dark:text-orange-500",
        danger: "text-red-900 dark:text-red-500",
      },
    },
  })({
    intent: props.intent,
  });
});
const contentClass = computed(() => {
  return cva("text-sm", {
    variants: {
      intent: {
        info: "text-blue-800 dark:text-blue-400",
        success: "text-green-800 dark:text-green-400",
        warning: "text-orange-800 dark:text-orange-400",
        danger: "text-red-800 dark:text-red-400",
      },
    },
  })({
    intent: props.intent,
  });
});
const closeButtonClass = computed(() => {
  return cva("p-0.5 rounded-lg -m-1", {
    variants: {
      intent: {
        info: "text-blue-900/70 hover:text-blue-900 hover:bg-blue-200",
        success: "text-green-900/70 hover:text-green-900 hover:bg-green-200",
        warning: "text-orange-900/70 hover:text-orange-900 hover:bg-orange-200",
        danger: "text-red-900/70 hover:text-red-900 hover:bg-red-200",
      },
    },
  })({
    intent: props.intent,
  });
});
const iconComponent = computed(() => {
  const icons = {
    info: InformationCircleIcon,
    success: CheckCircleIcon,
    warning: ExclamationTriangleIcon,
    danger: XCircleIcon,
  };

  return icons[props.intent];
});
const props = defineProps({
  intent: {
    type: String,
    validator(value) {
      return ["info", "success", "warning", "danger"];
    },
    default: "info",
  },
  title: {
    type: String,
  },
  show: {
    type: Boolean,
    default: true,
  },
  onDismiss: Function,
});

function dismiss() {
  if (props.onDismiss) {
    props.onDismiss();
  }
}
</script>

<template>
  <transition leave-action-class="duration-600" leave-to-class="opacity-0">
    <div v-if="props.show" :class="containerClass">
      <div class="shrink-0">
        <component :is="iconComponent" :class="iconClass" />
      </div>
      <div class="flex-1 space-y-2">
        <div :class="titleClass">
          {{ props.title }}
        </div>
        <div :class="contentClass">
          <slot></slot>
        </div>
      </div>
      <div class="shrink-0" v-if="props.onDismiss">
        <button @click="dismiss()" :class="closeButtonClass">
          <XMarkIcon class="w-6 h-6" />
        </button>
      </div>
    </div>
  </transition>
</template>

<style></style>
