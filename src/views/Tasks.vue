<template>
    <v-container grid-list-lg>
        <v-layout row wrap>
            <v-flex md6>
               <v-card class="my-3"  v-for="(item,index) in taskList" :key="index">
                   <v-chip label color="primary" text-color="white" class="ml-0">
                       <v-icon left>mdi-label</v-icon>
                       {{item.titulo}}
                   </v-chip>
                   <v-card-text>{{item.descripcion}}</v-card-text>
                   <v-card-actions>
                       <v-btn rounded color="warning" class="mx-2" @click="updateTask(index)">Editar</v-btn>
                       <v-btn rounded color="error" class="mx-2" @click="deleteTask(item.id)">Eliminar</v-btn>
                   </v-card-actions>
                    
               </v-card>

            </v-flex>
            <v-flex md6 v-if="formAdd">
               <v-card class="mb-3 pa-3">
                   <v-form @submit.prevent="addTask">
                       <v-text-field label="Título de la tarea" v-model="title"></v-text-field>
                       <v-textarea label="Descripcion" v-model="description"></v-textarea>
                       <v-btn block color="success" type="submit">agregar</v-btn>
                   </v-form>
               </v-card>
            </v-flex>

            <v-flex md6 v-if="!formAdd">
               <v-card class="mb-3 pa-3">
                   <v-form @submit.prevent="updateInfoTask">
                       <v-text-field label="Título de la tarea" v-model="title"></v-text-field>
                       <v-textarea label="Descripcion" v-model="description"></v-textarea>
                       <v-btn block color="warning" type="submit">Actualizar</v-btn>
                   </v-form>
               </v-card>
            </v-flex>
        </v-layout>

    <v-snackbar v-model="snackbar">
        {{ message }}
        <v-btn color="blue" text @click="snackbar = false">cerrar</v-btn>
    </v-snackbar>

    </v-container>
</template>

<script>
export default {
    data: () =>({
        taskList:[
            {id:1, titulo:'Tarea#1',descripcion:'primer comentario'},
            {id:2, titulo:'Tarea#2',descripcion:'segundo comentario'},
            {id:3, titulo:'Tarea#3',descripcion:'tercer comentario'}
        ],
        title:'',
        description:'',
        message: '',
        snackbar: false,
        formAdd:true,
        indexTask: ''
    }),
    methods:{
        addTask(){
            console.log(this.title, this.description)
            if(this.title === '' || this.description === ''){
                console.log('Empty fields')
                this.snackbar = true
                this.message = ' please fill all fields'
            }else{
                this.taskList.push({
                    id: Date.now(),
                    titulo: this.title,
                    descripcion: this.description
                })
                this.title = ''
                this.description = ''
                this.snackbar = true
                this.message ='Tarea Agregada'
            }
        },
        deleteTask(id){
            console.log(id)
            this.taskList = this.taskList.filter(el => el.id != id)
        },
        updateTask(index){
            this.formAdd = false
            this.title = this.taskList[index].titulo
            this.description = this.taskList[index].descripcion
            this.indexTask = index
        },
        updateInfoTask(){
            this.taskList[this.indexTask].titulo = this.title
            this.taskList[this.indexTask].descripcion = this.description
            this.formAdd = true
            this.title = ''
            this.description = ''
            this.snackbar = true
            this.message = 'info updated'
        }
    }
}
</script>