<template>
    <div class="container main">
        <Advertisement/>
        <div class="col-md-9">
            <ul class="breadcrumb">
                <li><router-link to="/">主页</router-link><span class="divider"></span></li>
                <li><router-link to="/category">管理栏目</router-link><span class="divider"></span></li>
                <li class="active">新建栏目</li>
            </ul>
            <div class="panel">
                <div class="inner">
                    <div class="topic_content">
                        <Alert v-if="alertObj" :data="alertObj"/>
                        <div class="markdown-text">
                            <h3>新建栏目</h3>
                            <form method="post" action="#" @submit.prevent="addCategory">
                                <div class="form-group">
                                    <div class="input-group">
                                        <div class="input-group-addon">栏目名称:</div>
                                        <input v-validate="'required'" data-vv-as="栏目名称" v-model="catName" type="text" class="form-control" name="catName" value="" placeholder="">
                                    </div>
                                    <span v-show="errors.has('catName')" class="errors">{{ errors.first('catName') }}</span>
                                </div>
                                <div class="form-group">
                                    <div class="input-group">
                                        <div class="input-group-addon">目录名称（小写英文字母）:</div>
                                        <input v-validate="'required'" data-vv-as="目录名称" v-model="catDir" type="text" class="form-control" name="catDir" value="" placeholder="">
                                    </div>
                                    <span v-show="errors.has('catDir')" class="errors">{{ errors.first('catDir') }}</span>
                                </div>
                                <div class="form-group">
                                    <div class="input-group">
                                        <div class="input-group-addon">目录简介:</div>
                                        <textarea v-model="catDesc" name="catDesc" class="form-control" rows="4" placeholder="请输入栏目简介，方便SEO优化"></textarea>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <div class="text-center">
                                        <button class="btn btn-success" type="submit">新建</button>
                                        <button class="btn btn-default" type="reset">清空</button>
                                    </div>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Advertisement from '../Advertisement'
    import Alert from '../Alert'

    export default {
        name: "CategoryAdd",
        components:{
            Advertisement,
            Alert,
        },
        data(){
            return {
                catName: '',
                catDir: '',
                catDesc:'',
                alertObj:null,
            }
        },
        methods:{
            addCategory(){
                this.$validator.validateAll().then((result) => {
                    if (result) {
                        // this.loading = true
                        this.$store.dispatch('addCategory', {
                            catName: this.catName,
                            catDir: this.catDir,
                            catDesc:this.catDesc,
                        })
                        .then((response) => {
                            //console.log(response.data)
                            this.alertObj=response.data
                        })
                        .catch(error => {
                            //this.loading = false
                            this.alertObj={status:false,msg:error.toString()}
                        })

                        return;
                    }
                    this.alertObj={status:false,msg:"请输入栏目信息"}
                });
            }
        }

    }
</script>

<style scoped>

</style>