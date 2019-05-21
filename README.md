# vue-otp-field
Input Field for OTP

## vue-otp-field props

| Props             | Type          | Default | Description                                                    |
| :---------------- |:------------- | :-------| :------------------------------------------------------------- |
| max               | Number        | `1`     | Max length for each input                                      |
| type              | String        | `tel`   | Type of each input                                             |
| placeholder       | String        | `●`     | Placeholder of each input                                      |
| onFieldCompleted  | Function      | `null`  | Callback function when user has completed (filled) all input   |
| amount            | Number        | `4`     | Amount of input field                                          |
| onFill            | Function      | `null`  | Callback function when user type in the value to the field     |

## Instalation
Install the package

```bash
yarn add vue-otp-field
```

or

```bash
npm install vue-otp-field
```

## Usage
```vue
<template>
  <div id="app">
    <div>
      <VueOTPField :onFieldCompleted="onFieldCompleted" :onFill="onFill" />
    </div>
  </div>
</template>

<script>
import VueOTPField from '@/components/VueOTPField'

export default {
  name: 'app',
  components: {
    VueOTPField
  },
  methods: {
    onFieldCompleted (value) {
      console.log('SUBMITTING')
    },
    onFill (inputObj) {
      console.log(inputObj)
    }
  }
}
</script>
```
`onFieldCompleted` method will trigger if the user already fill all the input, and you can get `value` of all the input

`onFill` method will trigger whenever user start filling the input, you will get the input object of

| Key              | Type    | Description                                           |
| :--------------- |:------- | :---------------------------------------------------- |
| currentValue     | String  | Current user typed input                              |
| isFieldsComplete | Boolean | The flag whether user has already fill all the input  |
| values           | String  | All input values combined                             |

## Example with button
```vue
<template>
  <div class="hello">
    <div class="container">
      <VueOTPField :onFill="onFill" />
      <button v-show="showButton" class="btn">Verify</button>
    </div>
  </div>
</template>

<script>
import VueOTPField from 'vue-otp-field'

export default {
  name: 'HelloWorld',
  data () {
    return {
      showButton: false
    }
  },
  components: {
    VueOTPField
  },
  props: {
    msg: String
  },
  methods: {
    onFill (val) {
      val.isFieldsComplete ? this.showButton = true : this.showButton = false
    }
  }
}
</script>
```

![example with button](https://raw.githubusercontent.com/maulanaahmadarif/vue-otp-field/master/wButton.gif)