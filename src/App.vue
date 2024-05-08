<script>
import { FontAwesomeIcon } from '../node_modules/@fortawesome/vue-fontawesome';
/* import font awesome icon component */
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

export default {
  components: {
    "font-awesome-icon": FontAwesomeIcon,
  },
  created(){
    console.log(FontAwesomeIcon);
  }
}
</script>

<template>
  <font-awesome-icon :icon="['fas', 'house']" />
</template>