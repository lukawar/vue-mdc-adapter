<template>
  <a class="mdc-toolbar__icon" 
    :class="{'material-icons':!!icon}"
    @click="dispatchEvent">
    <slot>{{icon}}</slot>
  </a>
</template>

<script>
import {DispatchEventMixin} from '../util'

export default {
  name: 'mdc-toolbar-icon',
  mixins: [DispatchEventMixin],
  props: {
    icon: String
  }
}
</script>
