<template>
  <v-app>
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="12" md="12" >
              <v-card class="elevation-0">
                <v-toolbar color="light-blue lighten-5"  >
                  <v-row justify="center">
                    <h3> ADD Contato</h3>
                  </v-row>
                </v-toolbar>
              </v-card>
              <v-form ref="form" v-model="valid" lazy-validation>
                <v-text-field
                  v-model="contatoData.nome" type="text" label="Nome" required>
                </v-text-field>
                <v-text-field
                  v-model="contatoData.sobrenome" type="text" label="Sobrenome" required>
                </v-text-field>
                <v-text-field
                  v-model="contatoData.email" type="text" label="E-mail" required>
                </v-text-field>
                <v-text-field
                  v-model="contatoData.telefone" type="text" label="Telefone" required>
                </v-text-field>
                <v-text-field
                  v-model="contatoData.endereco" type="text" label="Endereço" required>
                </v-text-field>
                <v-text-field
                  v-model="contatoData.cpf" type="text" label="CPF" required>
                </v-text-field>
                <v-btn color="primary" @click="saveContato()">
                  Salvar
                </v-btn>
              </v-form> <br>
              <v-card class="elevation-8"  >
                <v-toolbar color="teal accent-3" >
                  <v-row justify="center">
                    <h1>Lista de Contatos</h1>
                  </v-row>
                </v-toolbar>
              </v-card>
              <v-simple-table>
                <template v-slot:default>
                  <thead>
                    <tr>
                      <th class="text-center">Nome</th>
                      <th class="text-center">Sobrenome</th>
                      <th class="text-center">Email</th>
                      <th class="text-center">Telefone</th>
                      <th class="text-center">Endereço</th>
                      <th class="text-center">CPF</th>
                      <th class="text-center">Opções</th>
                    </tr>
                  </thead>
                <tbody>
                    <!-- <tr v-for="item in desserts" :key="item.name">-->
                  <tr v-for="contato in contatoList" :key="contato.cpf">
                      <td class="text-center">{{ contato.nome }}</td>
                      <td class="text-center">{{ contato.sobrenome }}</td>
                      <td class="text-center">{{ contato.email }}</td>
                      <td class="text-center">{{ contato.telefone }}</td>
                      <td class="text-center">{{ contato.endereco }}</td>
                      <td class="text-center">{{ contato.cpf }}</td>
                      <td class="text-center">
                        <v-btn class="mx-2" fab dark small color="primary" @click="editContato(contato)">
                          <v-icon dark>mdi-pencil</v-icon> 
                        </v-btn>
                        <v-btn class="mx-2" fab dark small color="error" @click="deleteContato(contato)">
                          <v-icon dark>mdi-delete</v-icon>
                        </v-btn>
                        </td>
                     </tr>
                </tbody>
              </template>
            </v-simple-table>
          </v-col>
       </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    contatoList: [],
    contatoData: {
     
      nome: "",
      sobrenome: "",
      email: "",
      telefone:"",
      endereco:"",
      cpf: ""
    }
    
    
  }),
  methods:{
      
      saveContato () {
      
      if(!this.contatoData.nome != ""&& !this.contatoData.sobrenome != "" && !this.contatoData.email != ""
          && !this.contatoData.telefone != "" && !this.contatoData.endereco != "" && !this.contatoData.cpf !="") {
            alert(' Compos obrigatórios!!!')
        }else{
          this.contatoList.push({...this.contatoData})
          alert(' Salvo com sucesso!!!')
        }
          this.contatoData = {}
        
      },
      
      editContato(contato){
        this.contatoData = { ...contato }
      },

    deleteContato (contato){
      this.contatoList = this.contatoList.filter(item => item.cpf !== contato.cpf)
       this.contatoData = {}
    }
       
  }
};
</script>
