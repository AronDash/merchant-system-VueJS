<template>
        <a-layout-content>
            <div class='card-one'>
                 <a-card title="User Setting">
                     <a-avatar style="backgroundColor:#1890ff" icon="user" size="large"/>
                     <div style="font-size: 20px; margin-bottom: 20px">
                        <span>Hi, {{username}}!</span> 
                    </div>
                     <a-button type="link" @click="handleDetail">
                     Change Detail
                    </a-button>
                    <a-button type="link" @click="handlePassword">
                     Change Password
                    </a-button>
                 </a-card>
            </div>   
            <!-- transition表示加动画 然后name代表class 在css里再添加animation -->
            <transition name="slide-fade">
            <div class="card-password" v-show="cardPasswordShow">
                 <a-card title="Change Password">
                    <a-form layout='vertical' :form="form">
                        <a-form-item label= 'Change Password'>  
                            <a-input-password type ='password' placeholder = 'Old Password'
                                 v-decorator="['password1',{rules: [{ required: true, message: 'Please input the old password' }],
                                 }]">
                            <a-icon slot='prefix' type="lock" style="color:rgba(0,0,0,.25)"/>
                            </a-input-password>
                        </a-form-item>
                        <a-form-item>  
                            <a-input-password type = 'password' placeholder = 'New Password'
                                 v-decorator="['password2',{rules: [{ validator: this.validatePwd}],
                                 }]">
                            <a-icon slot='prefix' type="lock" style="color:rgba(0,0,0,.25)"/>
                            </a-input-password>
                        </a-form-item>
                        <a-form-item>  
                            <a-input-password type = 'password' placeholder = 'Confirm Password'
                                 v-decorator="['password3',{rules: [{ required: true, message: 'Please confirm the password' }],
                                 }]">
                            <a-icon slot='prefix' type="lock" style="color:rgba(0,0,0,.25)"/>
                            </a-input-password>
                        </a-form-item>
                        <a-form-item>
                            <a-button type="primary" @click="changePassword">
                                Submit
                            </a-button>
                        </a-form-item>
                    </a-form>
                 </a-card>
            </div>
            </transition>   

             <transition name="slide-fade">
            <div class="card-detail" v-show="cardtDetailShow">
                 <a-card title="Change Detail">
                    <a-form layout='vertical' :form="form">
                        <a-form-item label= 'Change Password'>  
                            <a-input-password type ='password' placeholder = 'Old Password'
                                 v-decorator="['password1',{rules: [{ required: true, message: 'Please input the old password' }],
                                 }]">
                            <a-icon slot='prefix' type="lock" style="color:rgba(0,0,0,.25)"/>
                            </a-input-password>
                        </a-form-item>
                        <a-form-item>  
                            <a-input-password type = 'password' placeholder = 'New Password'
                                 v-decorator="['password2',{rules: [{ required: true, message: 'Please input the new password' }],
                                 }]">
                            <a-icon slot='prefix' type="lock" style="color:rgba(0,0,0,.25)"/>
                            </a-input-password>
                        </a-form-item>
                        <a-form-item>  
                            <a-input-password type = 'password' placeholder = 'Confirm Password'
                                 v-decorator="['password3',{rules: [{ required: true, message: 'Please confirm the password' }],
                                 }]">
                            <a-icon slot='prefix' type="lock" style="color:rgba(0,0,0,.25)"/>
                            </a-input-password>
                        </a-form-item>
                        <a-form-item>
                            <a-button type="primary">
                                Submit
                            </a-button>
                        </a-form-item>
                    </a-form>
                 </a-card>
            </div>
            </transition>    
        </a-layout-content>

</template>

<script>
    export default {
        
        data(){
            return {
              cardPasswordShow : false,
              cardtDetailShow : false,
              username: localStorage.getItem('username'),
            }
        },
         beforeCreate() {
           this.form = this.$form.createForm(this, { name: 'changepassword' });
        },
        created(){
                
        },
        methods:{
            
            handlePassword(){
                if(this.cardPasswordShow){
                    this.cardPasswordShow = false
                }
                else{
                    this.cardPasswordShow = true
                }
            },
            handleDetail(){
                this.cardtDetailShow = !this.cardtDetailShow 
            },
            changePassword(){
                this.form
            },
        }
    }
</script>

<style scoped>
    .ant-layout-content{
    padding: 0 100px;
    background-color: #f0f2f5;
  }
  .card-one{
    margin-top:40px;
    background-color: #f0f2f5;
    width:45%;
    box-shadow: 0px 1px 10px 5px rgba(17,17,17,0.1);
     float: left;

  }
  .card-password, .card-detail{
    margin-top:40px;
    background-color: #f0f2f5;
    width:40%;
    box-shadow: 0px 1px 10px 5px rgba(17,17,17,0.1);
    float: right;
  }
  .slide-fade-enter-active {
  transition: all 2s ease;
  }
  .slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }
  .slide-fade-enter, .slide-fade-leave-to {
  transform: translateX(10px);
  opacity: 0;
}

</style>