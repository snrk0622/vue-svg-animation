# vue-svg-like
A Vue component for animated like button
![preview](https://user-images.githubusercontent.com/87121234/139560465-74b3a30a-ee0b-48e3-bcf0-2ddd44cb172d.gif)
## Installation
NPM
```
npm install vue-svg-like
```
YARN
```
yarn add vue-svg-like
```

## Usage
```
<template>
  <vue-svg-like
    :clicked="clicked"
    color="#38b48b"
    subColor="#f08300"
    :size="5"
    :duration="0.5"
    @click="onClickLikeButton"
  />
</template>

<script>
import VueSvgLike from 'vue-svg-like'

export default {
  components: {
    VueSvgLike
  },
  data () {
    return {
      clicked: false
    }
  },
  methods: {
    onClickButtonLike: function () {
      this.clicked = !this.clicked 
    }
  }
}
</script>
```

## Configuration
| Property | Type | Description | Default |
| --- | --- | --- | --- |
| color | String | The main color. This color is assigned to the heart. | #f91880 |
| subColor | String | The sub color. This color is assigned to the explosion. | #f91880 |
| size | Number | Overall size of the button. This represents a multiple of the default size and should be a positive number. | 1 |
| duration | Number | Animation duration. This prepresents `animation-duration` in CSS and should be a positive number. The unit is s. | 1 |
| disabled | Boolean | This prevents the user from interacting with the button: it cannot be pressed or focused. | false |
