<template>
<article>
  <h1><code>&lt;veui-icon&gt;</code></h1>
  <div class="icons">
    <div
      v-for="icon in icons"
      :key="icon"
      class="icon"
    >
      <div class="svg">
        <veui-icon :name="icon"/>
      </div>
      <div class="name">
        {{ icon }}
      </div>
    </div>
  </div>
</article>
</template>

<script>
import bus from '../bus'
import { Icon } from 'veui'
import 'veui-theme-dls-icons'
import icons from 'veui-theme-dls-icons/icon-names.json'

export default {
  name: 'icon-demo',
  components: {
    'veui-icon': Icon
  },
  data () {
    return {
      icons
    }
  },
  mounted () {
    this.$children.forEach(child => {
      child.$on('click', () => {
        bus.$emit('log', child.$el.getAttribute('ui'))
      })
    })
  }
}
</script>

<style lang="less" scoped>
.icon {
  @grid-size: 100px;

  float: left;

  width: @grid-size;
  height: @grid-size + (0.8 + 0.6) * 16px;
  text-align: center;
  margin: 2em;

  .svg {
    width: @grid-size;
    height: @grid-size;
    border: 1px solid transparent;
    font-size: 1.6em;
    line-height: @grid-size;

    &:hover {
      border-color: #ccc;
    }
  }

  .name {
    margin-top: 0.6em;
    color: #333;
    font-size: 0.8em;
  }
}
</style>
