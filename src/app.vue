<script>
import Board from './components/board.vue'
import Login from './components/login.vue'

export default {
    name: "App",
    data() {
      return {
        isAuth: false,
        error: undefined,
        userData: null,
        users: [
          {
            login: 'admin',
            password: 'admin',
            avatar: 'https://cdn-icons-png.flaticon.com/512/5556/5556468.png'
          },
          {
            login: 'user1',
            password: 'user1',
            avatar: 'https://cdn-icons-png.flaticon.com/512/5556/5556468.png'
          },
          {
            login: 'user2',
            password: 'user2',
            avatar: 'https://static.vecteezy.com/system/resources/previews/009/397/892/original/woman-face-expression-clipart-design-illustration-free-png.png'
          }
        ]
      }
    },
    methods: {
      login(login, password){
        console.log('Авторизация');
        //Получить в методу, введенный пользователем логин и пароль
         console.log(login, password, this);
         // Ищем по введенному логину и паролю пользьзователя
         const component = this;
         const user = this.users.find(function(user){
            //Условие нахождения пользователя в массиве
            //Пароль и логин, должны подходить по условию, как минимум в одном объекте
            if(user.login == login && user.password == password){
                //isAuth - нужно изменить на true
                console.log(component)
                //component.isAuth = true;
                return user
            }
         })
         if (user) {
            //При успешном нахождении пользователя
            // 1 - возвращаем состояние ошибки в исходное
            // 2 - меняем флаг isAuth, который влияет на отображение определенного компонента
            // 3 - запишем данные пользователя для передачи в компонент board
            component.error = undefined
            component.isAuth = true;
            component.userData = user
         } else {
            component.error = 'Пользователь не найден';
         }
      },
      logout(){
          this.isAuth = false;
          this.userData = null
      }
    },
    components:{
      Board,
      Login
    }
}
</script>

<template>
  <Board test='Тестовый входящий параметр' :user="userData" :logout="logout" v-if="isAuth"/>
  <Login :handlerLogin='login' :error="error" v-else/>
  <div v-if="error" class="error">{{error}}</div>
</template>

<style scoped>
.error {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 24px;
  color: red;
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
