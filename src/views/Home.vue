<template>
  <div class="home">
    <color-block class="randomColor" :color="currentColor"></color-block>
    <div class="colorInfo">
      <p>Hex: <span class="colorHex">{{currentColor}}</span></p>
    </div>
    
    <button @click="getRandomColor()">next color</button>
    <div class="recentColors">
      <template v-for="color in recentColorsWithoutFirst">
        <color-block :key="color" class="recentColor" :color="color" display-hex></color-block>
      </template>
    </div>
    <foot></foot>
  </div>
</template> 

<script>
import ColorBlock from '../components/ColorBlock.vue';
import Foot from '../components/Footer.vue';

export default {
  name: 'home',
  data() {
    return {
      recentColors: [],
      currentColor: null,
    }
  },
  watch: {
    currentColor: function(newColor) {
      if(!newColor) return;

      this.recentColors.unshift(this.currentColor);
      localStorage.setItem('recentColors', JSON.stringify(this.recentColors));
    }
  },
  components: {
    Foot,
    ColorBlock
  },
  computed: {
    recentColorsWithoutFirst: function() {
      return this.recentColors.slice(1);
    }
  },
  methods: {
    getRandomColor: function() {
      let letters = '0123456789ABCDEF';
      let color = '#';

      for (let i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * 16)];
      }

      this.currentColor = color;

      return color;
    },
  },
  mounted: function() {
    this.getRandomColor();
    let colors = localStorage.getItem('recentColors');
    if (!colors) return;
    this.recentColors = JSON.parse(colors);
  }
}
</script>
