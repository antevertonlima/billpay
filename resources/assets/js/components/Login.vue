<template>
    <div class="content">
    <!--Echo out errors here. See example-->
    <!--<p class=error>Error, wrong email or password used. Please, try again.-->
    <form>
      <div class="mat-in">
        <input type="email" name="email" v-model="user.email" required></input>
        <span class="bar"></span>
        <label>E-mail</label>
      </div>
      <div class="mat-in">
        <input type="password" name="password" v-model="user.password" required></input>
        <span class="bar"></span>
        <label>Password</label>
      </div>
      <button type="button" name="submit" id="login" @click="login()">Login</button>
    </form>
  </div>

  <div class="bg-boxes">
    <svg width="300px" height="100%" id="col1">
      <rect width="150px" height="150px" x="75px" y="75px" class="bubble" id="bub1" />
    </svg>
    <svg width="200px" height="100%" id="col2">
      <rect width="100px" height="100px" x="50px" y="50px" class="bubble" id="bub2" />
    </svg>
    <svg width="260px" height="100%" id="col3">
        <rect width="130px" height="130px" x="65px" y="65px" class="bubble" id="bub3" />
    </svg>
    <svg width="160px" height="100%" id="col4">
        <rect width="80px" height="80px" x="40px" y="40px" class="bubble" id="bub4" />
    </svg>
    <svg width="240px" height="100%" id="col5">
        <rect width="120px" height="120px" x="60px" y="60px" class="bubble" id="bub5" />
    </svg>
    <!--Here is a triangle-->
    <svg width="200px" height="100%" id="col6">
        <polygon points="50,150 100,50 150,150" class="bubble" id="bub6" />
    </svg>
    <svg width="200px" height="100%" id="col7">
        <rect width="100px" height="100px" x="50px" y="50px" class="bubble" id="bub7" />
    </svg>
    <svg width="200px" height="100%" id="col8">
        <rect width="100px" height="100px" x="50px" y="50px" class="bubble" id="bub8" />
    </svg>
    <svg width="200px" height="100%" id="col9">
        <rect width="100px" height="100px" x="50px" y="50px" class="bubble" id="bub9" />
    </svg>
    <svg width="200px" height="100%" id="col10">
        <rect width="100px" height="100px" x="50px" y="50px" class="bubble" id="bub10" />
    </svg>
    <svg width="100px" height="100%" id="col11">
        <rect width="50px" height="50px" x="25px" y="25px" class="bubble" id="bub11" />
    </svg>
  </div>
</template>

<script>
    export default {
        data(){
            return {
                user:{
                    email: '',
                    password: ''
                }
            }
        },
        methods:{
            login(){
                this.$http.post('http://billpay.ddns.net/api/token',this.user)
                          .then((response) => {
                            window.localStorage.setItem('token', response.data.token);
                            this.$router.go({name: 'bill-pay.list'});
                            Materialize.toast('Logado com sucesso!', 4000);
                          })
            }
        },
        ready() {
            console.log('Component ready.')
        }
    }
</script>
