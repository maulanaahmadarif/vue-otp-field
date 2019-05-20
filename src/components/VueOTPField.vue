<template>
  <div class="vue-otp-container" :style="{ 'gridTemplateColumns': `repeat(${amount}, 1fr)` }">
    <div v-for="(number, index) in amount" :key="index" class="vue-otp-wrapper">
      <input class="vue-otp-field" :type="type" :maxlength="max" :placeholder="placeholder" @keyup="isNumber($event, index)" autocomplete="off" @focusin="onFocusIn($event, index)" >
    </div>
  </div>
</template>

<script>
export default {
  name: 'VueOTPField',
  data () {
    return {
      isFieldCompleted: false
    }
  },
  props: {
    max: {
      type: Number,
      default: 1
    },
    type: {
      type: String,
      default: 'tel'
    },
    placeholder: {
      type: String,
      default: '●'
    },
    amount: {
      type: Number,
      default: 4
    },
    onFieldCompleted: {
      type: Function
    },
    onFill: {
      type: Function
    }
  },
  methods: {
    onFocusIn (e, index) {
      const otpFields = document.querySelectorAll('.vue-otp-field')
      otpFields[index].value = ''
    },
    isNumber: function (e, index) {
      const numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
      const otpFields = document.querySelectorAll('.vue-otp-field')
      otpFields[index].setSelectionRange(0, 1)
      const selObj = window.getSelection()
      const selectedText = selObj.toString()
      const selectedValue = parseInt(selectedText, 10)
      if (numbers.indexOf(selectedValue) > -1) {
        otpFields[index].value = selectedValue
        if (index !== 3) {
          otpFields[index + 1].focus()
          otpFields[index + 1].value = ''
        }
      }
      if (selectedText === '') {
        otpFields[index].value = ''
        if (index !== 0) {
          otpFields[index - 1].focus()
          otpFields[index - 1].value = ''
        }
      }
      const inputValues = []
      otpFields.forEach((field) => {
        inputValues.push(field.value)
      })
      const isFieldsComplete = inputValues.every(value => value !== '')
      this.onFill({
        isFieldsComplete,
        currentValue: inputValues[index],
        values: inputValues.join('')
      })
      if (index === 3 && isFieldsComplete) {
        const values = inputValues.join('')
        this.onFieldCompleted(values)
      }
    }
  }
}
</script>


<style>
  .vue-otp-container {
    display: grid;
    align-items: center;
    justify-content: center;
  }

  .vue-otp-wrapper {
    display: flex;
    padding-left: 5px;
    padding-right: 5px;
  }

  .vue-otp-field {
    background: rgb(233,239,242);
    border-radius: 5px;
    border: 2px solid transparent;
    transition: all .1s ease-in;
    font-size: 1em;
    font-weight: 900;
    text-align: center;
    position: relative;
    width: 100%;
    min-height: 1px;
    padding-right: 5px;
    padding-left: 5px;
  }

  .vue-otp-field::-webkit-inner-spin-button, .vue-otp-field::-webkit-outer-spin-button {
    -moz-appearance: textfield;
    -webkit-appearance: none;
    margin: 0;
  }

  .vue-otp-field:active, .vue-otp-field:focus {
    outline: 0;
    box-shadow: none;
    background-color: transparent;
    border-color: #4c2a86;
  }

  .vue-otp-field:active::placeholder {
    opacity: 0;
  }

  .vue-otp-field:focus::placeholder {
    opacity: 0;
  }

  .vue-otp-field::placeholder {
    color: #abb6cb;
  }

  .vue-otp-field.otp--filled {
    background-color: rgba(76, 42, 134, .1);
  }
</style>
