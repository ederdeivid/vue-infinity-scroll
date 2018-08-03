# vue-infinity-scroll [![npm](https://img.shields.io/npm/v/vue-multiselect.svg)](https://www.npmjs.com/package/vue-infinity-scroll)
Probably the most complete *Infinity Scroll* component for Vue.js 2.0.

## NOTE:
 **All Versions before 1.0.5 doesn't work**

## Install & basic usage

```bash
npm i vue-infinity-scroll
```

```vue
<template>
  <div>
    <vue-infinity-scroll
      :hasNextPage="true"
      visClass="panel panel-default"
      visAllScreen="50vh"
      @scrolling="scrolling"
      buttonText="Go to Top"
      buttonClass="btn btn-primary"
      buttonIcon="fa fa-arrow-up"
    >
      // your things here
    </vue-infinity-scroll>
  </div>
</template>

<script>
import VueInfinityScroll from 'vue-infinity-scroll'

export default {
  data () {
    return {
      offset: 0,
    }
  },
  components: {
    VueInfinityScroll
  },
  methods: {
    scrolling () {
      this.offset = this.offset + 1
    }
  }
}

</script>
```

## All Properties
```bash
  :hasNextPage (Boolean) # Here u can use to see if u request has a next page to go
  @scrolling (Function) # that event is emited when the scroll down has ended
  :class (String) # Yor class
  :buttonText (String) # When u scroll down your vue-infinity-scroll u'll see a button to go to top, u can change the name of button using that props
  :buttonClass (String) # U can add yout class to button. Bootstrap example: "btn btn-sm btn-primary"
  :buttonIcon (String) # Icon to your button. Font-Awesome Example: "fa fa-arrow-up"
  :visSmallScreen (String) # When u resize your screen to a small screen (less than 768px) u can choose your height (vh, px, em...)
  :visMidScreen (String) # The same of visSmallScreen but to mid screen (between 768px and 1000px)
  :visLargeScreen (String) # The same of visSmallScreen but to large screen (bigger than 1000px)
  :visAllScreen (String) # Define only one height to all screen size
  :resetScroll (Boolean) # Can be util if u want do a new request and reset the current scroll (If u dont use, new request will jump to same before position)
```
