<template>
  <input type="text" v-model="value" @input="moneyMask">
</template>

<script>
import { 
  ref,
  toRefs,
  } from 'vue'

export default {
  
  props: ['default', 'modelValue'],

  setup(props, context) {
    const { emit } = context
    const $refs = toRefs(props)
    const modelValue = $refs.modelValue
    const vDefault = $refs.default
    const value = ref(props.modelValue || vDefault.value || '10010101')

    if (!modelValue.value) {
      value.value = vDefault.value || '10010101'
    }

    function formatMoney (val, signal = '') {
      if (!val)
        return signal + '0,00'

      if (typeof val === 'string')
        val = Number(val)

      return val.toFixed(2)
                .replace(/\d(?=(\d{3})+\.)/g, '$&.')
                .replace(/\.(\d\d)$/g, ',$1')
    }

    // From: https://github.com/beholdr/maska/blob/622316e5c3c3a05332fc249bb87a708a11a8982a/src/utils.js#L17
    function fixSelection (el, diff) {
      let position = el.selectionEnd + diff
      const digit = el.value[position - 1]

      while (position && position < el.value.length && el.value.charAt(position - 1) !== digit) {
        position++
      }

      if (el === document.activeElement) {
        setTimeout(function () {
          el.setSelectionRange(position, position)
        }, 0)
      }
    }

    function moneyMask ($event) {
      var value = String(this.value)

      // Add - signal into value
      if ($event.data === '-') value = '-' + value.replace(/-/g, '')
      else if ($event.data === '+') value = value.replace(/-/g, '')

      if (!value || value === '0,0') {
        this.value = ''
        emit('update:modelValue', null)
        return
      }

      var val = Number( (value.replace(/[^\d-]/g, '') || 0) / 100 )

      // Add money mask
      var signal = value.indexOf('-') === 0 ? '-' : ''
      this.value = formatMoney(val, signal)
      // this.value = window.$money(val, signal)

      // Update v-model
      emit('update:modelValue', this.value ? Number(this.value.replace(/\./g, '').replace(/,/g, '.')) : null)

      // update cursor position
      if (value.length > 1) {
        fixSelection($event.srcElement, this.value.length - value.length)
      }
    }

    value.value = formatMoney(value.value)

    return {
      value,
      moneyMask
    }
  }
  
}
</script>
