<template>
    <div>
        <form action="http://localhost:3005/users" method="post">
            <input type="text" name="name" v-model="name" placeholder="first name...">
            <input type="text" name="email" v-model="email" placeholder="email...">
            <input type="text" name="password" v-model="password" placeholder="password...">
            <input type="submit" value="send!">
        </form>
        <ul>
            <li>{{name}}</li>
            <li>{{email}}</li>
            <li>{{password}}</li>
            <li>{{this.password}}</li>
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
                users: {}
            }
        },
        methods: {
            allUsers: async function() {
                // let obj = {
                //     name: this.name,
                //     email: this.email,
                //     password: this.password
                // }
                // console.log(obj);
                // try {
                //     await fetch('http://localhost:3005/users', {
                //         method: 'post',
                //         body: JSON.stringify(obj)
                //     })
                //     .then((res) => res.json())                    
                //     .then(function(data) {
                //         console.log(data);
                //     });
                //     // const users = await res.json();
                //     // this.users = users;
                // } catch (e) {
                //     console.log(e)
                // };
            },
            // sendData: async function() {
            //     try {
            //         const send = await fetch(`https://localhost:3005/`);
            //     } catch (e) {
            //         console.log(e)
            //     }
            // }
        }
    }
</script>

<style lang="scss" scoped>

</style>