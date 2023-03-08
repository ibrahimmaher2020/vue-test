<template>
  <form @submit.prevent="handleSubmit">   
    <label >Email address :</label>
    <input type="email " required v-model="email">
    <label >Password:</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError" class=" text-danger p-2  text-center">{{ passwordError }}</div>
    <label >Role:</label>
    <select v-model="role">
        <option value="Developer">Web Developer</option>
        <option value="Designer">Web designer</option>
    </select>
    <label >Skills -
        <span style="color:brown">  Tyep <strong> ',' </strong> to add text -</span>
    </label>
    <input type="text" v-model="tempSkills" @keyup="addSkill">
    
    <div v-for="skill in skills" :key="skill" class="pill">
          
        <span  @click="delSkil(skill)"> {{skill}}</span>
        
    </div>

    <div class="terms">
        <input type="checkbox" v-model="terms" required>
        <label >Accept terms and condtions</label>       
    </div>
   <div class="submit">
        <button class="btn btn-warning ">Create an Account</button>
   </div>
    
  </form>
  <p>email : {{ email  }}</p>
  <p>password : {{ password  }}</p>
  <p>Role : {{ role  }}</p>
  <p>terms : {{ terms}}</p>  

</template>

<script>


export default {
    
    data(){
        return{
            email:'ibrahim',
            password:'',
            role:'Designer',
            terms:false,  
            tempSkills:'',
            skills:[],
            passwordError:''
            
        }
    },
    methods:{
        addSkill(e){

            if (e.key===',' && this.tempSkills) {
                this.tempSkills=this.tempSkills.substring(0,this.tempSkills.length-1)//delete Comma
                
                if (!this.skills.includes(this.tempSkills)){
                    //this.skills.push(this.tempSkills.substring(0,this.tempSkills.length-1))                    
                    this.skills.push(this.tempSkills)                    
                }
                console.log(e);
                this.tempSkills=''
            }           
        },
        delSkil(T){
           this.skills=this.skills.filter(item=>item!==T)

        },
        handleSubmit(){
           this.passwordError=this.password.length<6?'Password must be at least 5 chars log':''

        }
    }
    
}
</script>

<style>
form{

    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;    
}
label{
    color:#aaa;
    display:inline-block;
    margin: 25px 0 15px;
    font-size: 0.9em;
    text-transform: capitalize;
    letter-spacing: 1px;
    font-weight: bold;
}
input,select {
    display: block;
    padding: 10px 6px;
    width:100%;
    box-sizing: border-box;
    border:none;
    border-bottom: 1px solid #ddd;
    color:#555;
}
input[type="checkbox"]{
    display: inline-block;
    width:16px;
    margin : 0 10px 0 0;
    position:relative;
    top:2px;

}
.pill{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color:#777;
    cursor: pointer;

}
button{
    border-radius: 20px;    
}
.submit{
    text-align: center;
}
</style>