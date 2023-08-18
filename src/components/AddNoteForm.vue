<template>
  <div id="app">
<div>
  <table>
    <tr> <td><meta itemprop="image" content="http://your-link.png"></td> <td></td><td> </td></tr>
    <tr>
      <td><p v-for="(cat,n) in cats">
        <span class="cat">{{ cat }}</span>
      </p></td>
      <td></td>
      <td><p  v-for="(dog,n) in dogs">
        <span class="dog">{{ dog }}</span>
        &nbsp;&nbsp;<button @click="removeDogCat(n)">Удалить</button>
      </p></td>
    </tr>
  </table>
  </div>
    Тема
    <p>
      <input v-model="newCat">
    </p>
    Основной текст
    <p>
    <textarea v-model="newDog"></textarea>
    </p>
    <button @click="addDogCat">Добавить заметку</button>
  </div>
</template>

<script>
export default {
  data() {

    return {
      cats: [],
      newCat: null,
      dogs: [],
      newDog: null,
      source:{}
    }
  },
  mounted() {
    if (localStorage.getItem('cats')) {
      try {
        this.cats = JSON.parse(localStorage.getItem('cats'));
      } catch(e) {
        localStorage.removeItem('cats');
      }
    }
    if (localStorage.getItem('dogs')) {
      try {
        this.dogs = JSON.parse(localStorage.getItem('dogs'));
      } catch(e) {
        localStorage.removeItem('dogs');
      }
    }
  },
  methods: {
    addDogCat() {
      // ensure they actually typed something
      if (!this.newDog && !this.newCat) {
        return;
      }
      this.dogs.push(this.newDog);
      this.newDog = '';
      this.cats.push(this.newCat);
      this.newCat = '';
      this.saveDogs();
      this.saveCats();
    },
    removeDogCat(x) {
      this.dogs.splice(x, 1);
      this.cats.splice(x, 1);
      this.saveDogs();
      this.saveCats();
    },
    saveDogs() {
      const parsed = JSON.stringify(this.dogs);
      localStorage.setItem('dogs', parsed);
    },
    saveCats() {
      const parsed = JSON.stringify(this.cats);
      localStorage.setItem('cats', parsed);
    }

  }
}
</script>

<style lang="scss" scoped>
input {
  width: 400px;
}
textarea{
  width: 400px;
  height: 100px;
}
.form-fields {
  margin-right: 50px;
  margin-bottom: 50px;
}
</style>
<script setup>
</script>