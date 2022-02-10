<template>
  <div class="hello">
    <h1>dropdown autocomplete</h1>
      <input class="dropdown-input" type="text" name="autocomplete" v-model="filteredInputValue" v-on:keyup.up="keyUp" v-on:keyup.down="keyDown" v-on:keyup.enter="keyEnter" v-on:keyup.esc="resetItemClick()" @focus="listDisplayed = true">
      <a
        href="#"
        @click.prevent="resetItemClick()"
      > X </a>

      <div class="dropdown-content" v-if="listDisplayed">
        <ul class="dropdown-items">
          <li :ref="'list_'+item.id" v-for="item in items" :key="item.id" :class="item.id === idHoverSelectedElement ? 'selected' : 'unselected'">
            <a
              href="#"
              @click.prevent="handleItemClick(item, $event)"
            >{{ item.text }}</a>
          </li>
        </ul>
      </div>
  </div>
</template>

<script>
export default {
  name: 'DropdownListAutocomplete',
  props: {
    dropdowndata: Array
  },
  data () {
    return {
      items: this.dropdowndata,
      filteredInputValue: '',
      selectedElement: null,
      indexHoverSelectedElement: null,
      idHoverSelectedElement: null,
      listDisplayed: false
    }
  },
  watch: {
    filteredInputValue(val) {
      this.items = this.dropdowndata.filter(el => el.text.includes(val))
    }
  },
  methods: {
    handleItemClick(item) {
      this.selectedElement = item;
      this.filteredInputValue = item.text;
      this.listDisplayed = false;
      this.$emit('selected', item);
    },
    resetItemClick() {
      this.selectedElement = null;
      this.filteredInputValue = '';
      this.items = this.dropdowndata;
      this.listDisplayed = true;
    },
    keyUp() {
      if (this.indexHoverSelectedElement === null || this.indexHoverSelectedElement === 0) {
        this.indexHoverSelectedElement = this.items.length - 1;
      } else {
        this.indexHoverSelectedElement--;
      }
      this.idHoverSelectedElement = this.items[this.indexHoverSelectedElement].id;
      const key = 'list_'+this.idHoverSelectedElement;
      this.$refs[key][0].scrollIntoView();
    },
    keyDown() {
      if (this.indexHoverSelectedElement === null || this.indexHoverSelectedElement === this.items.length-1) {
        this.indexHoverSelectedElement = 0;
      } else {
        this.indexHoverSelectedElement++;
      }
      this.idHoverSelectedElement = this.items[this.indexHoverSelectedElement].id;
      const key = 'list_'+this.idHoverSelectedElement;
      this.$refs[key][0].scrollIntoView();
    },
    keyEnter() {
      if (this.selectedElement === null) {
        this.selectedElement = this.items[this.indexHoverSelectedElement];
        this.filteredInputValue = this.items[this.indexHoverSelectedElement].text;
        this.$emit('selected', this.items[this.indexHoverSelectedElement]);
        this.listDisplayed = false;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.dropdown-input {
  color: black;
  border: 1px solid gray;
  border-radius: 15px;
  padding: 0 5px;
  line-height: 30px;
}

.dropdown-content {
  position: relative;
}

ul {
  list-style: none;
  padding: 10px 0;
  margin: auto;
  height: 10rem;
  overflow-y: scroll;
  width: 15rem;
}

li {
  margin: 0.2rem;
  border: 1px solid gray;
  background: none;
  margin: auto;
  width: 12rem;
}

.selected {
  background-color: #34568B;
}
</style>
