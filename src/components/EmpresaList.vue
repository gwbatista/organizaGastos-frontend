<template>
  <v-card class="pa-3" style="max-width: 100%;">
    <v-toolbar flat>
      <v-toolbar-title>Empresa</v-toolbar-title>
      <v-divider class="mx-4" inset vertical></v-divider>
      <v-spacer></v-spacer>
      <v-dialog v-model="dialog" max-width="500px">
        <template v-slot:activator="{ props }">
          <v-btn class="mb-2" color="primary" dark v-bind="props">
            Adicionar Gasto
          </v-btn>
        </template>
        <v-card>
          <v-card-title>
            <span class="text-h5">{{ formTitle }}</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <v-col cols="12" md="12" sm="6">
                  <v-text-field v-model="editedItem.descricao" label="Descrição"></v-text-field>
                </v-col>
                <v-col cols="12" md="12" sm="6">
                  <v-text-field v-model="editedItem.data_vencimento" label="Data de Vencimento"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.janeiro" label="Janeiro"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.fevereiro" label="Fevereiro"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.marco" label="Março"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.abril" label="Abril"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.maio" label="Maio"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.junho" label="Junho"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.julho" label="Julho"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.agosto" label="Agosto"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.setembro" label="Setembro"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.outubro" label="Outubro"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.novembro" label="Novembro"></v-text-field>
                </v-col>
                <v-col cols="12" md="4" sm="6">
                  <v-text-field v-model="editedItem.dezembro" label="Dezembro"></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue-darken-1" variant="text" @click="close">Cancelar</v-btn>
            <v-btn color="blue-darken-1" variant="text" @click="save">Salvar</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <v-dialog v-model="dialogDelete" max-width="500px">
        <v-card color="red">
          <v-card-title class="text-h11">Tem certeza de que deseja deletar este gasto?</v-card-title>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="black" variant="text" @click="closeDelete">Cancelar</v-btn>
            <v-btn color="black" variant="text" @click="deleteItemConfirm">OK</v-btn>
            <v-spacer></v-spacer>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-toolbar>
    
    <v-data-table
      :headers="headers"
      :items="gastos"
      class="elevation-1"
      style="width: 100%;"
      :sort-desc="false"
      item-key="id"
    >

    <template v-slot:item.janeiro="{ item }">
  <v-chip 
    :color="item.janeiroPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'janeiro')"
    outlined
  >
    {{ item.janeiro }}
  </v-chip>
</template>

<template v-slot:item.fevereiro="{ item }">
  <v-chip 
    :color="item.fevereiroPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'fevereiro')"
    outlined
  >
    {{ item.fevereiro }}
  </v-chip>
</template>

<template v-slot:item.marco="{ item }">
  <v-chip 
    :color="item.marcoPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'marco')"
    outlined
  >
    {{ item.marco }}
  </v-chip>
</template>

<template v-slot:item.abril="{ item }">
  <v-chip 
    :color="item.abrilPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'abril')"
    outlined
  >
    {{ item.abril }}
  </v-chip>
</template>

<template v-slot:item.maio="{ item }">
  <v-chip 
    :color="item.maioPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'maio')"
    outlined
  >
    {{ item.maio }}
  </v-chip>
</template>

<template v-slot:item.junho="{ item }">
  <v-chip 
    :color="item.junhoPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'junho')"
    outlined
  >
    {{ item.junho }}
  </v-chip>
</template>

<template v-slot:item.julho="{ item }">
  <v-chip 
    :color="item.julhoPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'julho')" 
    outlined
  >
    {{ item.julho }}
  </v-chip>
</template>

<template v-slot:item.agosto="{ item }">
  <v-chip 
    :color="item.agostoPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'agosto')"
    outlined
  >
    {{ item.agosto }}
  </v-chip>
</template>

<template v-slot:item.setembro="{ item }">
  <v-chip 
    :color="item.setembroPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'setembro')" 
    outlined
  >
    {{ item.setembro }}
  </v-chip>
</template>

<template v-slot:item.outubro="{ item }">
  <v-chip 
    :color="item.outubroPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'outubro')" 
    outlined
  >
    {{ item.outubro }}
  </v-chip>
</template>

<template v-slot:item.novembro="{ item }">
  <v-chip 
    :color="item.novembroPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'novembro')" 
    outlined
  >
    {{ item.novembro }}
  </v-chip>
</template>

<template v-slot:item.dezembro="{ item }">
  <v-chip 
    :color="item.dezembroPago ? 'green' : 'grey'" 
    @click="togglePago(item, 'dezembro')" 
    outlined
  >
    {{ item.dezembro }}
  </v-chip>
</template>


      <template v-slot:item.acao="{ item }">
        <v-icon class="me-2" size="small" @click="editItem(item)">mdi-pencil</v-icon>
        <v-icon size="small" @click="deleteItem(item)">mdi-delete</v-icon>
      </template>
    </v-data-table>
  </v-card>

  <v-dialog v-model="showTotals" max-width="500px">
  <template v-slot:activator="{ props }">
    <v-btn color="primary" style="margin-top: 16px; margin-bottom: 16px;"  v-bind="props">
      Total - Empresa
    </v-btn>
  </template>
  
  <v-card color="orange">
    <v-card-title>Total por Mês - Empresa</v-card-title>
    <v-card-item>
      <div class="card-total">Janeiro: R$ {{ totalJaneiro.toFixed(2) }}</div>
      <v-divider color="white" ></v-divider>
      <div class="card-total">Fevereiro: R$ {{ totalFevereiro.toFixed(2) }}</div>
      <v-divider color="white" ></v-divider>
      <div class="card-total">Março: R$ {{ totalMarco.toFixed(2) }}</div>
      <v-divider color="white" ></v-divider>
      <div class="card-total">Abril: R$ {{ totalAbril.toFixed(2) }}</div>
      <v-divider color="white" ></v-divider>
      <div class="card-total">Maio: R$ {{ totalMaio.toFixed(2) }}</div>
      <v-divider color="white" ></v-divider>
      <div class="card-total">Junho: R$ {{ totalJunho.toFixed(2) }}</div>
      <v-divider color="white" ></v-divider>
      <div class="card-total">Julho: R$ {{ totalJulho.toFixed(2) }}</div>
      <v-divider color="white" ></v-divider>
      <div class="card-total">Agosto: R$ {{ totalAgosto.toFixed(2) }}</div>
      <v-divider color="white" ></v-divider>
      <div class="card-total">Setembro: R$ {{ totalSetembro.toFixed(2) }}</div>
      <v-divider color="white" ></v-divider>
      <div class="card-total">Outubro: R$ {{ totalOutubro.toFixed(2) }}</div>
      <v-divider color="white" ></v-divider>
      <div class="card-total">Novembro: R$ {{ totalNovembro.toFixed(2) }}</div>
      <v-divider color="white" ></v-divider>
      <div class="card-total">Dezembro: R$ {{ totalDezembro.toFixed(2) }}</div>
    </v-card-item>
    <v-card-actions>
      <v-btn color="gray" @click="showTotals = false">Fechar</v-btn>
    </v-card-actions>
  </v-card>
</v-dialog>

</template>

<script>
export default {
  data: () => ({
    showTotals: false,
    dialog: false,
    dialogDelete: false,
    headers: [
      { title: 'Descrição', value: 'descricao', fixed: true},
      { title: 'Vencimento', value: 'data_vencimento', sortable: true},
      { title: 'Janeiro', value: 'janeiro' },
      { title: 'Fevereiro', value: 'fevereiro' },
      { title: 'Março', value: 'marco' },
      { title: 'Abril', value: 'abril' },
      { title: 'Maio', value: 'maio' },
      { title: 'Junho', value: 'junho' },
      { title: 'Julho', value: 'julho' },
      { title: 'Agosto', value: 'agosto' },
      { title: 'Setembro', value: 'setembro' },
      { title: 'Outubro', value: 'outubro' },
      { title: 'Novembro', value: 'novembro' },
      { title: 'Dezembro', value: 'dezembro' },
      { title: 'Ações', value: 'acao', sortable: false },
    ],
    gastos: [],
    editedIndex: -1,
    editedItem: {
      descricao: '',
      valor: 0,
      data_vencimento: '',
      janeiro: 0,
      fevereiro: 0,
      marco: 0,
      abril: 0,
      maio: 0,
      junho: 0,
      julho: 0,
      agosto: 0,
      setembro: 0,
      outubro: 0,
      novembro: 0,
      dezembro: 0,
      pago: false,
      janeiroPago: false,
      fevereiroPago: false,
      marcoPago: false,
      abrilPago: false,
      maioPago: false,
      junhoPago: false,
      julhoPago: false,
      agostoPago: false,
      setembroPago: false,
      outubroPago: false,
      novembroPago: false,
      dezembroPago: false,
    },
    defaultItem: {
      descricao: '',
      valor: 0,
      data_vencimento: '',
      janeiro: 0,
      fevereiro: 0,
      marco: 0,
      abril: 0,
      maio: 0,
      junho: 0,
      julho: 0,
      agosto: 0,
      setembro: 0,
      outubro: 0,
      novembro: 0,
      dezembro: 0,
      pago: false,
      janeiroPago: false,
      fevereiroPago: false,
      marcoPago: false,
      abrilPago: false,
      maioPago: false,
      junhoPago: false,
      julhoPago: false,
      agostoPago: false,
      setembroPago: false,
      outubroPago: false,
      novembroPago: false,
      dezembroPago: false,
    },
  }),

  computed: {
    formTitle () {
      return this.editedIndex === -1 ? 'Novo Gasto' : 'Editar Gasto';
    },
    totalJaneiro() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.janeiro) || 0, 0);
  },
  totalFevereiro() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.fevereiro) || 0, 0);
  },
  totalMarco() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.marco) || 0, 0);
  },
  totalAbril() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.abril) || 0, 0);
  },
  totalMaio() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.maio) || 0, 0);
  },
  totalJunho() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.junho) || 0, 0);
  },
  totalJulho() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.julho) || 0, 0);
  },
  totalAgosto() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.agosto) || 0, 0);
  },
  totalSetembro() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.setembro) || 0, 0);
  },
  totalOutubro() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.outubro) || 0, 0);
  },
  totalNovembro() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.novembro) || 0, 0);
  },
  totalDezembro() {
    return this.gastos.reduce((total, item) => total + parseFloat(item.dezembro) || 0, 0);
  },
  },

  watch: {
    dialog (val) {
      val || this.close();
    },
    dialogDelete (val) {
      val || this.closeDelete();
    },
  },

  async mounted() {
    // Carrega os dados dos gastos quando o componente é montado
    const response = await fetch('http://localhost:3000/empresa');
    this.gastos = await response.json();
  },

  created () {
    this.carregarGastos();
  },

  methods: {
    toggleTotals() {
    this.showTotals = !this.showTotals;
  },
    async carregarGastos() {
  try {
    const response = await fetch('http://localhost:3000/empresa');
    if (!response.ok) {
      throw new Error('Erro ao buscar gastos');
    }
    const data = await response.json();
    console.log(data); // Veja os dados que estão sendo retornados
    this.gastos = data.map(item => ({
      ...item,
      janeiroPago: item.janeiro_pago,
      fevereiroPago: item.fevereiro_pago,
      marcoPago: item.marco_pago,
      abrilPago: item.abril_pago,
      maioPago: item.maio_pago,
      junhoPago: item.junho_pago,
      julhoPago: item.julho_pago,
      agostoPago: item.agosto_pago,
      setembroPago: item.setembro_pago,
      outubroPago: item.outubro_pago,
      novembroPago: item.novembro_pago,
      dezembroPago: item.dezembro_pago
    }));
  } catch (error) {
    console.error('Erro ao carregar gastos:', error);
  }
},

    async save() {
      if (this.editedIndex > -1) {
        // Atualizar gasto existente
        await this.atualizarGasto(this.editedItem);
        Object.assign(this.gastos[this.editedIndex], this.editedItem);
      } else {
        // Adicionar novo gasto
        const newItem = await this.adicionarGasto();
        this.gastos.push({ ...this.editedItem, id: newItem.id });
      }
      this.close();
    },

    async adicionarGasto() {
      try {
        const response = await fetch('http://localhost:3000/empresa', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(this.editedItem)
        });
        if (!response.ok) {
          throw new Error('Erro ao adicionar gasto');
        }
        const data = await response.json();
        return data; // Retorna o novo item com o ID
      } catch (error) {
        console.error('Erro ao adicionar gasto:', error);
      }
    },

    async atualizarGasto(item) {
      try {
        const response = await fetch(`http://localhost:3000/empresa/${item.id}`, {
          method: 'PUT',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(item)
        });
        if (!response.ok) {
          throw new Error('Erro ao atualizar gasto');
        }
      } catch (error) {
        console.error('Erro ao atualizar gasto:', error);
      }
    },

    async togglePago(item, mes) {
  try {
    const campoPago = `${mes}Pago`; // Cria o nome do campo de pagamento baseado no mês
    const novoStatus = !item[campoPago]; // Inverte o status de pagamento

    // Faz a requisição PUT para atualizar o backend
    await fetch(`http://localhost:3000/empresa/${item.id}/${mes}`, {
      method: 'PUT',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ pago: novoStatus }), // Envia o novo status como 'pago'
    });

    // Atualiza o status localmente após a resposta do backend
    item[campoPago] = novoStatus;
    await this.carregarGastos();
  } catch (error) {
    console.error('Erro ao atualizar o status de pagamento:', error);
  }
},


    editItem(item) {
      this.editedIndex = this.gastos.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.gastos.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    async deleteItemConfirm() {
      await this.deletarGasto(this.editedItem.id);
      this.gastos.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    async deletarGasto(id) {
      try {
        const response = await fetch(`http://localhost:3000/empresa/${id}`, {
          method: 'DELETE'
        });
        if (!response.ok) {
          throw new Error('Erro ao deletar gasto');
        }
      } catch (error) {
        console.error('Erro ao deletar gasto:', error);
      }
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },
  },
};
</script>

<style scoped>
.title {
  font-weight: bold;
  font-size: 20px;
  margin-bottom: 14px;
}

span {
  padding: 14px
}

.card-total {
  margin-bottom: 3px;
  margin-top: 3px;
}
</style>
