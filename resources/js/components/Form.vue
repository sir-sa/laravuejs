<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Company Details</div>

                    <div class="card-body">
                    	<div v-for="s in success" class="alert alert-success">
                    		<strong>{{s}}</strong>
                    	</div>
                    	<div v-for="e in errors" class="alert alert-danger">
                    		<strong>{{e}}</strong>
                    	</div>
                        <form>
                        	Name: <input type="text" v-model="name" class="form-control">
                        	Phone: <input type="number" v-model="phone" class="form-control">
                        	Email: <input type="email" v-model="email" class="form-control">
                        	<input type="submit" @click.prevent="createcompany()" >
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
    	data(){
    		return{
    			success: null,
    			errors: null,
    			name: '',
    			email: '',
    			phone: ''
    		}
    	},
    	methods: {
    		createcompany(){
                if (!this.name) {
                	this.errors=['Name cannot be empty'] 
                	return false;
                }
                if (!this.phone) {
                	this.errors=['phone cannot be empty']
                	return false;
                }
                if (!this.email) {
                	this.errors=['email cannot be empty']
                	return false;
                }else if(!this.validEmail(this.email)){
                	this.errors=['please enter valid email']
                	return false;
                }

                axios.post('./company',{nam:this.name, phone:this.phone,email:this.email}).then(response=>{
                	this.success=response.data;
                }).catch(errors=>{
                	this.errors= errors.data;
                })

    		},
    		validEmail: function (email) {
			    var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
			    return re.test(email);
			}
    	},
        mounted() {
            alert('welcome');
        }
    }
</script>
