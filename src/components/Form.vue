<template>
    <div id="container">
        <form action="http://localhost:3005/users" method="post">
            <div id="inputs">
                <input id="name" class="inputs" type="text" name="name" v-model="name" placeholder="first name...">
                <input id="email" class="inputs" type="text" name="email" @change="this.emailIsValid" v-model="email" placeholder="email...">
                <input id="password" class="inputs" type="text" name="password" @change="this.userInputs" v-model="password" placeholder="password...">
                <button id="button" class="inputs" type="submit" value="send!" ref="button">
                    <font-awesome-icon v-if="this.show === true && this.validity === true" id="check" icon="check-circle"></font-awesome-icon>
                    <font-awesome-icon v-else-if="this.show === true && this.validity === false" id="cross" icon="times-circle"></font-awesome-icon>
                    <font-awesome-icon v-else id="userEdit" icon="user-edit"></font-awesome-icon>
                        Go!
                    <font-awesome-icon id="arrow" icon="angle-double-right"></font-awesome-icon>
                </button>
                <div id="alerts">
                    <p v-if="this.validity === false && this.inputsEdited === true" id="indicator">Invalid e-mail address</p>
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
            }
        },
        methods: {
            emailIsValid: function (email) {
                email = this.email
                
            
                this.validity = /\S+@\S+\.\S+/.test(email)
                console.log(`emailIsValid:${this.validity}`)
                this.send();
            },
            userInputs: function() {
                if (this.name !== '' && this.email !== '' && this.password !== '') {
                    this.inputsEdited = true
                    this.show = true
                }

                console.log(`userInputs:${this.inputsEdited}`)
            },
            send: function() {
                let send = this.$refs.button;
                if (this.validity === true && this.inputsEdited === true) {
                    send.style.color = '#2ed573';
                } else if (this.validity === false && this.inputsEdited === true) {
                    send.style.color = '#ff4757';
                }
            },
            

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
    justify-content: center;
    align-items: center;
    background-color:#5352ed;
    border-radius: 7%;
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