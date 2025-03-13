<template>
  <div class="container">
    <h1>Выберите или введите текст</h1>
    <div class="input-wrapper">
      <div class="combobox">
        <input 
          v-model="inputText" 
          type="text" 
          class="text-input" 
          placeholder="Выберите или введите текст..."
          @input="handleInput"
          @focus="showOptions = true"
          @blur="handleBlur"
        >
        <div v-if="showOptions" class="options-list">
          <div 
            v-for="option in filteredOptions" 
            :key="option" 
            class="option"
            @click="selectOption(option)"
            @mouseover="hoveredOption = option"
          >
            {{ option }}
          </div>
        </div>
      </div>
      <p v-if="inputText" class="input-preview">Вы выбрали: {{ inputText }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      inputText: '',
      showOptions: false,
      hoveredOption: null,
      options: [
        'Первый вариант',
        'Второй вариант',
        'Третий вариант',
        'Четвертый вариант',
        'Пятый вариант'
      ]
    }
  },
  computed: {
    filteredOptions() {
      if (!this.inputText) return this.options
      return this.options.filter(option => 
        option.toLowerCase().includes(this.inputText.toLowerCase())
      )
    }
  },
  methods: {
    handleInput() {
      console.log('Введенный текст:', this.inputText)
    },
    selectOption(option) {
      this.inputText = option
      this.showOptions = false
    },
    handleBlur() {
      setTimeout(() => {
        this.showOptions = false
      }, 200)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.input-wrapper {
  margin-top: 20px;
  position: relative;
}

.combobox {
  position: relative;
  width: 100%;
}

.text-input {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 2px solid #42b983;
  border-radius: 4px;
  font-size: 16px;
  transition: all 0.3s ease;
  background-color: white;
}

.text-input:focus {
  outline: none;
  border-color: #2c3e50;
  box-shadow: 0 0 5px rgba(66, 185, 131, 0.3);
}

.options-list {
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  background: white;
  border: 1px solid #42b983;
  border-radius: 4px;
  margin-top: 4px;
  max-height: 200px;
  overflow-y: auto;
  z-index: 1000;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.option {
  padding: 10px 20px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.option:hover {
  background-color: #f0f0f0;
}

.input-preview {
  margin-top: 10px;
  color: #42b983;
  font-weight: bold;
}

h1 {
  color: #2c3e50;
  margin-bottom: 30px;
}
</style>
