<script>

    export default{
        //props: ["onTagsChange"],
        emits: ["onTagsChange"],
        data(){
            return{
                currenValue: '',
                tags:[]
            }
        },
        methods: {
            handleKeyDown(e){
                console.log(e.key)
                if(e.key === 'Backspace' && this.currenValue === ''){
                    this.tags.pop()
                    //this.onTagsChange(this.tags)
                    this.$emit('onTagsChange', this.tags)
                }
            },
            handleSubmit(){
                if(this.currenValue != ''){
                    const exist = this.tags.some((items) => items === this.currenValue)   
                    console.log(exist)                 
                    if(!exist){
                        this.tags.push(this.currenValue)
                        console.log(this.tags)
                        this.currenValue = ''
                        //this.onTagsChange(this.tags)
                        this.$emit('onTagsChange', this.tags)
                    }                    
                }
            },
            deleteTag(tag){
                this.tags = this.tags.filter((item) => item != tag)   
                console.log(this.tags)
                //this.onTagsChange(this.tags)
                this.$emit('onTagsChange', this.tags)
            }
        },

    }

</script>

<template>
    <div class="inputTag">
        <div class="tags">
            <div class="tag" v-for="(tag, index) in tags" :key="index">
                {{ tag }} <button @click="deleteTag(tag)">X</button>
            </div>
        </div>
        <form @submit.prevent="handleSubmit">
            <input class="input" type="text" v-model="currenValue" @keydown="handleKeyDown">
        </form>
    </div>
</template>

<style scoped>

.inputTag{
    display: inline-flex;
    border: solid 1px #000;
    border-radius: 3px;
    height: 43px;
}
.inputTag .input{
    border: none;
    outline: none;
    padding: 0 5px;
}
.inputTag form{
    display: inline-flex
}
.tags{
    display: flex;
    gap: 3px;
    padding: 5px;
}
.tags .tag{
    display: flex;
    padding: 5px;
    border: solid 1px #ccc;
    gap: 5px;
    align-content: center;
    border-radius: 3px;
}
.inputTag button{
    background-color: transparent;
    border: none;
    border-radius: 3px;
    cursor: pointer;
}
.tag button:hover{
    background-color: #ccc;
}
</style>