<template>
    <div id="container">
        <form action="http://localhost:3005/users" method="post">
            <h1 id="title">Sign Up</h1>
            <div id="inputs">
                <div id="user">
                    <input id="name" class="inputs" type="text" name="name" v-model="name" autocomplete="off" placeholder="username...">
                    <input id="email" class="inputs" type="text" name="email" @keydown="this.emailIsValid" v-model="email" autocomplete="off" placeholder="email...">
                    <input id="password" class="inputs" ref="pass" type="password" name="password" @keyup="this.userInputs" v-model="password" autocomplete="off" placeholder="password...">
                    <button id="button" class="inputs" type="submit" value="send!" ref="button">
                        <font-awesome-icon v-if="this.show === true && this.validity === true" id="check" icon="check-circle"></font-awesome-icon>
                        <font-awesome-icon v-else-if="this.show === true && this.validity === false" id="cross" icon="times-circle"></font-awesome-icon>
                        <font-awesome-icon v-else id="userEdit" icon="user-edit"></font-awesome-icon>
                            Go!
                        <font-awesome-icon id="arrow" icon="angle-double-right"></font-awesome-icon>
                    </button>
                </div>
                <div id="validation">
                    <div id="passwordToggle">
                        <input type="checkbox" @click="this.togglePassword">
                        <div v-if="this.visibilePassword === false">show password</div>
                        <div v-else>hide password</div>
                    </div>
                    <div id="alerts">
                        <p v-if="this.validity === false && this.inputsEdited === true" id="indicator">The provided email address is not valid</p>
                    </div>
                </div>
            </div>
        </form>
        <ul>
            <!-- <li>{{name}}</li>
            <li>{{email}}</li>
            <li>{{password}}</li>
            <li>{{this.password}}</li> -->
        </ul>
    </div>
</template>

<script>

    export default {
        name: 'Form',
        data() {
            return {
                name: '',
                email: '',
                password: '',
                users: {},
                show: false,
                validity: false,
                inputsEdited: false,
                visibilePassword: false
            }
        },
        methods: {
            emailIsValid: function (email) {
                email = this.email;
                
            
                this.validity = /\S+@\S+\.\S+/.test(email);
                console.log(`emailIsValid:${this.validity}`);
                this.send();
            },
            userInputs: function() {
                if (this.name !== '' && this.email !== '' && this.password !== '') {
                    this.inputsEdited = true;
                    this.show = true;
                }

                console.log(`userInputs:${this.inputsEdited}`)
                this.send();
            },
            send: function() {
                let send = this.$refs.button;
                if (this.validity === true && this.inputsEdited === true) {
                    send.style.color = '#2ed573';
                } else if (this.validity === false && this.inputsEdited === true) {
                    send.style.color = '#ff4757';
                }
            },
            togglePassword: function() {
                let pass = this.$refs.pass;
                console.log(pass.type);

                if (pass.type === "password") {
                    pass.type = "text";
                    this.visibilePassword = true;
                } else {
                    pass.type = "password";
                    this.visibilePassword = false;
                }
            }

        }
    }
</script>

<style scoped>
#container {
    width: 30vw;
    height: 40vw;
    display: flex;
    justify-content: center;
    align-items: center;
    /* background-color:#ced6e0; */
    /* padding: 10px;
    border-radius: 7%; */
}
form {
    height: 75%;
    width: 75%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color:#5352ed;
    border-radius: 7%;
    box-shadow: 0px 0px 30px 2px #1e3799;
}
#title {
    color: white;
    text-shadow: 2px 2px 5px #70a1ff
}
input:focus,
button:focus {
    outline:none;
}
#inputs {
    display: flex;
    flex-direction: column;
    width: 75%;
    height: 75%;
    justify-content: space-between
}

#user {
    height: 80%;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
}
#validation {
    height: 20%;
    width: 100%;
}
#alerts {
    height: 25%;
}
.inputs {
    height: 10%;
    border: 0;
    padding: 5px;
    border-radius: 20px;
    font-size: 2vh;
    padding-left: 1vw;
}

#button {
    display: flex;
    justify-content: space-between;
    padding: 0 1vw 0 1vw;
    align-items: center;
    color: #747d8c;
    box-shadow: 5px 5px 20px 5px #3742fa;
}

#passwordToggle {
    width: 50%;
    display: flex;
    justify-content: space-between;
}

#check {
    color: #2ed573;
}
#cross {
    color: #ff4757;
}

#arrow {
    color: #70a1ff;
}

#indicator {
    color: #ff4757;
}
</style>