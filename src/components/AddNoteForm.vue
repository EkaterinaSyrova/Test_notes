<template>
  <div id="app">
    <div>
      <table>
        <tr><td>Тема</td><td>Основной текст</td><td>Картинка</td><td>Удалить заметку</td></tr>
        <tr>
          <td>
            <p v-for="(cat,n) in cats">
            <span class="cat">{{ cat }}</span></p>
          </td>
          <td>
            <p  v-for="(dog,n) in dogs">
            <span class="dog">{{ dog }}</span>></p>
          </td>
          <td>
            <p v-for="(pic,n) in pics">
            <img :src="pic"/></p>
          </td>
          <td>
            <p  v-for="(dog,n) in dogs">
              <button id="remove" @click="removeDogCat(n)">Удалить</button>
       </p>
          </td>
        </tr>
      </table>
      <br>
    </div>
    <h2>Добавить новую заметку</h2>
    Тема
    <p>
      <input v-model="newCat">
    </p>
    Основной текст
    <p>
      <textarea v-model="newDog"></textarea>
    </p>
    Картинка
    <p>
      <input v-model="newPic">
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
      pics:[],
      newPic: null
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
    if (localStorage.getItem('pics')) {
      try {
        this.pics = JSON.parse(localStorage.getItem('pics'));
      } catch(e) {
        localStorage.removeItem('pics');
      }
    }
  },
  methods: {
    addDogCat() {
      // ensure they actually typed something
      if (!this.newDog && !this.newCat && !this.newPic) {
        return;
      }
      this.dogs.push(this.newDog);
      this.newDog = '';
      this.cats.push(this.newCat);
      this.newCat = '';
      this.pics.push(this.newPic);
      this.newPic = '';
      this.saveDogs();
      this.saveCats();
      this.savePics();
    },
    removeDogCat(x) {
      this.dogs.splice(x, 1);
      this.cats.splice(x, 1);
      this.pics.splice(x, 1);
      this.saveDogs();
      this.saveCats();
      this.savePics();
    },
    saveDogs() {
      const parsed = JSON.stringify(this.dogs);
      localStorage.setItem('dogs', parsed);
    },
    saveCats() {
      const parsed = JSON.stringify(this.cats);
      localStorage.setItem('cats', parsed);
    },
    savePics() {
      const parsed = JSON.stringify(this.pics);
      localStorage.setItem('pics', parsed);
    }

  }
}
</script>

<style lang="scss" scoped>
input {
  width: 400px;
}
img{
  width: 50px;
}
tr{
  height: 100px;
  border: 1px solid black;
}
table{
  border: 1px solid black;
}
td{
  width: 400px;
  border: 1px solid black;
  text-align: center;
  vertical-align: top;
}
textarea{
  width: 400px;
  height: 100px;
}
.remove{
  margin-left: auto;
  margin-right: 0;
}
.form-fields {
  margin-right: 50px;
  margin-bottom: 50px;
}
</style>
