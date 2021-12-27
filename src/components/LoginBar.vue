<template>
    <div class="login">
        <div class="leftBar">
            <div class="topText">
                <h1>{{text.mainText}}</h1>
                <p>{{text.subText}}</p>
            </div>
            <div class="inputBar">
                <h5 class="userText">{{text.usern}}</h5>
                <input class="userInput" type="text" placeholder="Username" v-model="user.userName">
                <h5 class="passwordText">{{text.pass}}</h5>
                <input class="passwordInput" type="password" placeholder="Password" v-model="user.password">
            </div>
                <img class="Quotes" src="../assets/images/Quotes.png" alt="">
            <div class="signIn">
                <div class="signup">
                    <a class="signUpA" @click="isVisible = !isVisible">{{text.signUp}}</a>
                    <a class="signUpA">{{text.fPass}}</a>
                </div>
                <button class="btn" @click="signIn">{{text.signIn}}</button>
            </div>
        </div>
        <div class="rightBar">
            <h1>{{text.make}} <br> {{text.dream}}</h1>
            <p>{{text.rightSubText}}</p>
        </div>
        <div
        :class="[isVisible ? 'signUp' : 'aSignUp']">
            <img @click="isVisible = !isVisible" class="closeSignUp" src="../assets/images/close.png">
            <form>
                <label class="userText labels">
                    Username
                </label>
                    <input v-model="signUp.userName" class="userInput" type="text" placeholder="Username">
                <label class="userText labels">
                    E-mail
                </label>
                    <input v-model="signUp.eMail" class="userInput" type="email" placeholder="E-mail">
                <label class="userText labels">
                    Password
                </label>
                    <input v-model="signUp.password" class="userInput" type="password" placeholder="Password">
                <button class="btnSignUp" @click="signUpMethods">Sign Up</button>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            isVisible:false,
            text:{
                mainText: 'Welcome to ToDo',
                subText: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Omnis pariatur deleniti neque officia.',
                rightSubText: '"Lorem ipsum dolor sit, amet consectetur adipisicing elit. Sit necessitatibus officia autem quo dicta! Magnam quis mollitia doloremque repellendus architecto."',
                usern:'Username',
                pass:'Password',
                fPass:'Forgot Password',
                signUp:'Sign Up',
                signIn:'Sign In',
                make:'Make a',
                dream:"Dream.",
            },
            user:{
                userName:"",
                password:"",
            },
            signUp:{
                userName:"",
                password:"",
                eMail:"",
            }
        }
    },
    methods: {
        signIn(){
            this.$http.get("https://vue-social-todo-default-rtdb.firebaseio.com/users.json")
            .then((response) =>{
                let data= response.body;
                console.log(response.body);
                for(let key in data){
                    console.log(data[key].userName);
                    console.log(data[key].password);
                    if(data[key].userName==this.userName && data[key].password==this.password){
                        alert("Giriş Başarili")
                        break;
                    } else{
                        alert("Hatali Giriş")
                    }
                }
            })
        },
        signUpMethods(){
            this.$http.post("https://vue-social-todo-default-rtdb.firebaseio.com/users.json",{
                userName:this.signUp.userName,
                password:this.signUp.password,
                eMail:this.signUp.eMail,
            })
            .then((response) =>{
                alert("Kayıt Başarili")
                console.log(response.body);
            })
        }
    }
}
</script>