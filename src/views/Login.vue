<template>
	<div>
		<div class="divlogin">
	        <div class="container">
	            <div class="divcont">
	                <h3>{{ title }}</h3>
	                <form @submit.prevent="sendForm()">
	                    <input type="email" :class="{'error':validaEmail}" placeholder="Email" v-model="form.email">
	                    <input type="password" v-if="form.type!=2" :class="{'error':validaPassword}" placeholder="Contraseña" v-model="form.password" >
	                    <input type="password" v-if="form.type==1" :class="{'error':validaRepetirPassword}" placeholder="Repetir contraseña" v-model="form.passwordos" >
	                    <button>Iniciar sesión</button>
	                    <a href="javascript:void(0)" @click="form.type=2" v-if="form.type!=2" >Recuper contraseña</a>
	                    <a href="javascript:void(0)" @click="form.type=1" v-if="form.type!=1" >Registrarme</a>
	                    <a href="javascript:void(0)" @click="form.type=0" v-if="form.type!=0" >Iniciar sesión</a>
	                </form>
	            </div>
	        </div>
    	</div>
    </div>
</template>

<script>
export default {
	name: 'login',
	data() {
		return {
			form:{
            type:0, // 0 = Login , 1 = Registro 2- Recuperar contraseña
            email:"",
            password:"", 
            passwordos:""}
		}
	},
    methods:{
        sendForm(){
            if(this.validaType()){
                console.log(this.form);
            }
        },
        validaType(){
            if(this.form.type==0 && !this.validaEmail && !this.validaPassword){
                return true;
            }
            else if(this.form.type==1 && !this.validaEmail && !this.validaRepetirPassword){
                return true;
            }
            else if(this.form.type==2 && !this.validaEmail){
                return true;
            }
            return false;
        }
    },
    computed:{
        validaEmail(){
            var exp = /^(([^<>()[\]\.,;:\s@\"]+(\.[^<>()[\]\.,;:\s@\"]+)*)|(\".+\"))@(([^<>()[\]\.,;:\s@\"]+\.)+[^<>()[\]\.,;:\s@\"]{2,})$/i;
            if(exp.test(this.form.email)){
                return false;
            } else{
                return true;
            }
        },
        validaPassword(){
            var exp = /^(?=.*\d)(?=.*[a-záéíóúüñ]).*[A-ZÁÉÍÓÚÜÑ]/;
            if(exp.test(this.form.password)){
                return false;
            } else{
                return true;
            }
        },
        validaRepetirPassword(){
            if(this.form.password==this.form.passwordos){
                return false;
            } else{
                return true;
            }
        },
        title(){
            return (this.form.type==0)?'Login':(this.form.type==1)?'Registro':'Recuperar contraseña';
        }
    }
}
</script>

<style>
	@import url('https://fonts.googleapis.com/css?family=Roboto');

	html,body{ padding: 0px; margin: 0px; width: 100%; height: 100vh; font-family: "Roboto"; color:#333;  }
	.divlogin{ 
	    background: url(../assets/fondo.jpg);
	    background-size: cover; 
	    background-position: center center; 
	    width: 100%; 
	    height: 100vh; 
	    display: flex;
	    align-content: center;
	    align-items: center;    
	}
	.divlogin .container{ 
	    width: 100%;
	    text-align: center;
	}
	.divlogin .container .divcont{
	    width: 100%;
	    max-width: 300px;
	    background: rgba(255,255,255,0.7);
	    padding: 20px;
	    border-radius: 10px;
	    display: inline-block;
	}
	.divlogin .container .divcont h3{
	    margin-top: 0px;
	}
	.divlogin .container .divcont input{ 
	    height: 30px; 
	    margin: 0px; 
	    border: 0px; 
	    outline: none; 
	    padding: 10px; 
	    border-radius: 5px; 
	    width: 90%;
	    margin-bottom: 10px;
	}
	.divlogin .container .divcont input.error{ border-bottom: 3px solid red; }
	.divlogin .container .divcont button{ 
	    margin: 0px; 
	    border:0px; 
	    display: block; 
	    margin: auto; 
	    padding: 10px 30px;
	    background: #333;
	    color:#fff;
	    border-radius: 5px;
	    margin-bottom: 10px;
	}
	.divlogin .container .divcont a{
	    font-size: 12px;
	    margin-right: 10px;
	    color:#333;
	}
</style>