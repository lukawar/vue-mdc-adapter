<template>
  <a :href="href" class="mdc-drawer-item mdc-list-item" 
    :class="classes" :style="styles"
    @click="onClick">
    <span class="mdc-list-item__start-detail" v-if="hasStartDetail">
      <slot name="start-detail">
        <i class="material-icons" aria-hidden="true">{{startIcon}}</i>
      </slot>
    </span>
    <slot></slot>
  </a>
</template>

<script>
import {RippleBase, DispatchEventMixin} from '../util'

export default {
  name: 'mdc-drawer-item',
  inject: ['mdcDrawer'],
  mixins: [DispatchEventMixin],
  props: {
    'start-icon': String,
    'href': String,
    'temporary-close': {type: Boolean, default: true}
  },
  data () {
    return {
      classes: {},
      styles: {}
    }
  },
  computed: {
    hasStartDetail () {
      return this.startIcon || this.$slots['start-detail']
    }
  },
  methods: {
    onClick (evt) {
      this.mdcDrawer.isTemporary && this.temporaryClose 
        && this.mdcDrawer.close()
      this.dispatchEvent(evt)
    }
  },
  mounted () {
    this.ripple = new RippleBase(this)
    this.ripple.init()
  },
  beforeDestroy () {
    this.ripple && this.ripple.destroy()
    this.ripple = null
  }
}
</script>
