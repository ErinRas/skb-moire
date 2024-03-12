<template>
  <base-form-radio :group="group">
    <span class="options__value">
      {{ title }} <b v-if="+price">{{ `${pricePretty} ₽` }}</b> <b v-else>бесплатно</b>
    </span>
  </base-form-radio>
</template>

<script>
import BaseFormRadio from '@/components/BaseFormRadio.vue'
import numberFormat from '@/helpers/numberFormat.js'

export default {
  components: { BaseFormRadio },
  props: ['title', 'price', 'group'],
  computed:{
    pricePretty(){
return numberFormat(this.price)
    }
  }
}
</script>
