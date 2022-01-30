<template>
  <div class="clsCommon">
    <div id="divSearch">
      Search: <input type="text" class="clsCommon" v-model="search" ref="search" autofocus/>
      <input type="checkbox" v-model="checkedDisabled"/> Disable remove buttons
      <input type="radio" v-model="filterPosition" value="startsWith">Starts With
      <input type="radio" v-model="filterPosition" value="endsWith">Ends With
      <input type="radio" v-model="filterPosition" value="contains" checked>Contains
    </div>
    <div class="colors-div">
      <div v-for="(color, index) in filteredList" :key="color" >
        <div class="single-color" :style="{'background-color': color}" >
          <div>
            <img src="./assets/star_off.svg" width="15px" v-if="!favorites.includes(index)" @click="favoriteColorSwitch(color)">
            <img src="./assets/star_on.svg" width="15px" v-if="favorites.includes(index)" @click="favoriteColorSwitch(color)">
            {{color}}
          </div>

          <button :class="[ { 'buttonClicked': checkedDisabled} ]" @click="removeFromArray(color)" :disabled="checkedDisabled">{{removeButton}}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      colors: ["Black", "Navy", "DarkBlue", "MediumBlue", "Blue", "DarkGreen", "Green", "Teal", "DarkCyan", "DeepSkyBlue",
        "DarkTurquoise", "MediumSpringGreen", "Lime", "SpringGreen", "Aqua", "Cyan", "MidnightBlue", "DodgerBlue",
        "LightSeaGreen", "ForestGreen", "SeaGreen", "DarkSlateGray", "DarkSlateGrey", "LimeGreen", "MediumSeaGreen",
        "Turquoise", "RoyalBlue", "SteelBlue", "DarkSlateBlue", "MediumTurquoise", "Indigo", "DarkOliveGreen",
        "CadetBlue", "CornflowerBlue", "RebeccaPurple", "MediumAquaMarine", "DimGray", "DimGrey", "SlateBlue",
        "OliveDrab", "SlateGray", "SlateGrey", "LightSlateGray", "LightSlateGrey", "MediumSlateBlue", "LawnGreen",
        "Chartreuse", "Aquamarine", "Maroon", "Purple", "Olive", "Gray", "Grey", "SkyBlue", "LightSkyBlue", "BlueViolet",
        "DarkRed", "DarkMagenta", "SaddleBrown", "DarkSeaGreen", "LightGreen", "MediumPurple", "DarkViolet", "PaleGreen",
        "DarkOrchid", "YellowGreen", "Sienna", "Brown", "DarkGray", "DarkGrey", "LightBlue", "GreenYellow",
        "PaleTurquoise", "LightSteelBlue", "PowderBlue", "FireBrick", "DarkGoldenRod", "MediumOrchid", "RosyBrown",
        "DarkKhaki", "Silver", "MediumVioletRed", "IndianRed", "Peru", "Chocolate", "Tan", "LightGray", "LightGrey",
        "Thistle", "Orchid", "GoldenRod", "PaleVioletRed", "Crimson", "Gainsboro", "Plum", "BurlyWood", "LightCyan",
        "Lavender", "DarkSalmon", "Violet", "PaleGoldenRod", "LightCoral", "Khaki", "AliceBlue", "HoneyDew", "Azure",
        "SandyBrown", "Wheat", "Beige", "WhiteSmoke", "MintCream", "GhostWhite", "Salmon", "AntiqueWhite", "Linen",
        "LightGoldenRodYellow", "OldLace", "Red", "Fuchsia", "Magenta", "DeepPink", "OrangeRed", "Tomato", "HotPink",
        "Coral", "DarkOrange", "LightSalmon", "Orange", "LightPink", "Pink", "Gold", "PeachPuff", "NavajoWhite",
        "Moccasin", "Bisque", "MistyRose", "BlanchedAlmond", "PapayaWhip", "LavenderBlush", "SeaShell", "Cornsilk",
        "LemonChiffon", "FloralWhite", "Snow", "Yellow", "LightYellow", "Ivory", "White"],
      search: '',
      checkedDisabled: false,
      removeButton: 'Remove',
      filterPosition: 'contains',
      favorites: [],
      favoriteStatus: false
    }
  },
  computed: {
    filteredList() {
      return this.colors.filter(color => {
        if(this.filterPosition === 'startsWith') {
          return color.toLowerCase().startsWith(this.search.toLowerCase())
        }
        else if(this.filterPosition === 'endsWith') {
          return color.toLowerCase().endsWith(this.search.toLowerCase())
        } else {
          return color.toLowerCase().includes(this.search.toLowerCase())
        }
      })
    }
  },
  methods: {
    focusInput() {
      this.$refs.search.$el.focus();
    },
    removeFromArray(colorToRemove) {
      let index = this.colors.indexOf(colorToRemove);
      if (index !== -1) {
        this.colors.splice(index, 1);
      }
    },
    favoriteColorSwitch(state) {
      let index = 0;
      let colorIndex = this.colors.indexOf(state)
      if (colorIndex !== -1) {
        if(this.favorites.includes(colorIndex)){
          while (index < this.favorites.length) {
            if (this.favorites[index] === this.colors.indexOf(state)) {
              this.favorites.splice(index, 1);
            } else {
              ++index;
            }
          }
        } else {
          this.favorites.push(colorIndex)
        }
      }
    }
  }
}
</script>

<style>
.clsCommon {
  font-size: 20px;
  font-family: arial;
  text-align: left;
}
.single-color {
  padding: 0px;
  margin-top: 5px;
  margin-bottom: 5px;
  border: 1px solid gray;
  border-radius: 10px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.colors-div {
  margin-top: 6%;
}

#divSearch {
  position: fixed;
  top: 1%;
  left: 8px;
  right: 6px;
  text-align: left;
  background-color: lightgray;
  padding: 10px;
  border-radius: 10px;
}
INPUT{
  border-radius: 10px;
  padding: 5px
}
BUTTON {
  background-color: #337ab7;
  color: #fff;
  border: 1px solid #2e6da4;
  border-radius: 5px;
  padding: 6px 12px;
  font-size: 16px;
}

.buttonClicked{
  padding: 6px 12px;
  font-size: 16px;
  border: 1px solid #999999;
  background-color:#CCC;
  color: #666666;
}
</style>