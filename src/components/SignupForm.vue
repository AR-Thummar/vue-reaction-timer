<template>
    <form @submit.prevent="handleSubmit">
        <label>Email:</label>
        <input type="email" v-model="email" required>

        <label>Password:</label>
        <input type="password" v-model="password" required>
        <div v-if="passwordError" class="error">{{ passwordError }}</div>
        <div v-for="suggestion in passwordSuggestions" :key="suggestion">
            <span>{{ suggestion }}</span>
        </div>

        <label>Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label>Skills (press alt + comma to add):</label>
        <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{ skill }}</span>
        </div>
        <p>You have {{ numberOfPreferedSkill }} skills that we needed.</p>

        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label>Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Create an Account</button>
        </div>
    </form>
</template>
  
<script>
export default {
    data() {
        return {
            email: 'test@gmail.com',
            password: '',
            role: 'developer',
            terms: false,
            skills: [],
            tempSkill: '',
            passwordError: null,
            preferedSkills: ['Node.js', 'Vue.js', 'React.js', 'SQL'],
            numberOfPreferedSkill: 0,
            passwordSuggestions: []
        }
    },
    methods: {
        addSkill($event) {
            if ($event.key === ',' && this.tempSkill) {
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ''
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter(item => {
                return skill !== item
            })
        },
        handleSubmit() {
            // validate password
            this.passwordError = this.password.length > 5 ?
                '' : 'Password must be at least 6 characters long'

            if (!this.passwordError) {
                console.log('email: ', this.email)
                console.log('password: ', this.password)
                console.log('role: ', this.role)
                console.log('skills: ', this.skills)
                console.log('terms accepted: ', this.terms)
            }
        }
    },
    // In Vue.js, the watch allows you to observe changes in reactive properties 
    // and perform custom logic when those properties change.
    // Use Case: Asynchronous Data Fetching
    watch: {
        password(newPassword) {
            console.log(newPassword)
            const suggestions = [];

            if (!/[a-z]/.test(newPassword)) {
                suggestions.push('Include lowercase letters');
            }
            if (!/[A-Z]/.test(newPassword)) {
                suggestions.push('Include uppercase letters');
            }
            if (!/\d/.test(newPassword)) {
                suggestions.push('Include numbers');
            }
            if (!/[!@#$%^&*(),.?":{}|<>]/.test(newPassword)) {
                suggestions.push('Include special characters');
            }

            this.passwordSuggestions = suggestions;
        }
    }
}
</script>
  
<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input,
select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}

.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}

button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}

.submit {
    text-align: center;
}

.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>