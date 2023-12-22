<template>
  <div class="chinese-traditional-colors">
    <header class="header">
      <h1
        class="title"
        @click="currentColor = 'transparent'"
      >
        中国传统色
      </h1>
    </header>

    <section
      v-for="series of colors"
      :key="series.type"
      class="series"
    >
      <header class="series-header">
        <h2
          class="series-title"
          @click="currentColor = 'transparent'"
        >
          {{ series.name }}
        </h2>
      </header>

      <ul class="colors">
        <li
          v-for="color of series.colors"
          :key="color.name"
          class="color-item"
          :class="series.type"
          :data-color="color.name"
          :style="`--color: #${color.color}`"
          @click="handleClick(color)"
        >
          <h3 class="name">{{ color.name }}</h3>
          <div class="hex">#{{ color.color }}</div>
        </li>
      </ul>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

import colors from './colors/colors.json'

const currentColor = ref('transparent')

const handleClick = (color: any) => {
  currentColor.value = `#${color.color}`
  navigator.clipboard.writeText(`#${color.color}`)
}
</script>

<style lang="scss">
* { margin: 0; padding: 0; box-sizing: border-box; }

.chinese-traditional-colors {
  background-color: v-bind(currentColor);
  transition: all linear 1s;
  overflow: hidden;

  > .header {
    text-align: center;
  }

  .series {
    width: 80%;
    margin: 64px auto;

    .series-header {
      text-align: center;
    }

    .colors {
      display: flex;
      flex-wrap: wrap;
      list-style: none;
      margin-top: 16px;

      .color-item {
        position: relative;
        width: 25%;
        height: 80px;
        padding: 16px;
        color: #fff;
        background-color: var(--color);
        background-image: url(./assets/2.png);
        background-size: 100px;
        background-repeat: no-repeat;
        background-position: right bottom;
        border: 1px solid #f1f1f1;
        cursor: pointer;

        &.white {
          color: #000;
        }
      }
    }
  }
}
</style>
