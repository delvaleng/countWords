<template>
  <v-container fluid>

    <v-spacer class="pa-2"></v-spacer>
    <v-card
      :elevation="8"
      class="pa-3 flexcard d-flex flex-column rounded-lg"
      color="gray"
      height="100%"
    >
    <v-card-subtitle class="pb-0">
      <div class="pb-3 font-weight-bold">Contador de Palabras</div>
    </v-card-subtitle>

    <v-card-text>
      <v-form
        ref="form"
        v-model="valid"
        lazy-validation
      >
        <v-row>
          <v-col
            cols="12"
            md="6"
            >
            <v-text-field
              v-model="palabra"
              outlined
              label="Ingresa tu palabra a contar"
              placeholder="Palabra..."
              required
              :rules="palabraRules"
              >
            </v-text-field>
            <v-textarea
              v-model="texto"
              outlined
              auto-grow
              label="Ingresa tu texto aquí"
              placeholder="Texto a contar"
              required
              :rules="textoRules"
            >
            </v-textarea>

          </v-col>
          <v-col
            cols="12"
            md="6"
            >
            <div>Cantidad de Palabras :<span class="pb-3 font-weight-bold" > {{ countTotal }} </span>  </div>
            <div>Otras Palabras:</div>

            <ul id="example-2">
              <li v-for="(item, index) in countWords" :key="index">
                <span class="pb-3 font-weight-bold" >{{ index }} </span> :  {{ item }}
              </li>
            </ul>
          </v-col>

        </v-row>
      </v-form>
    </v-card-text>

      <v-row
        align="center"
        justify="space-around"
        >
        <v-col
          cols="12"
          md="6"
          >
          <v-btn
            color="warning"
            depressed
            block
            outlined
            elevation="8"
            @click="reset"
          >
            Limpiar
          </v-btn>
        </v-col>

        <v-col
          cols="12"
          md="6"
          >
          <v-btn
            color="primary"
            depressed
            block
            outlined
            elevation="8"
            @click="count(texto, palabra)"

          >
            Contar
          </v-btn>
        </v-col>

      </v-row>
    </v-card>


  </v-container>
</template>

<script>
export default {
  data () {
    return {
      valid      : null,
      countTotal : 0,
      countWords : [],
      texto      : '',
      palabra    : '',
      textoRules: [
        v => !!v || 'Este campo es requerido.',
      ],
      palabraRules: [
        v => !!v || 'Este campo es requerido.',
      ],
    }
  },
  methods: {
    reset () {
      this.$refs.form.reset()
    },
    count: function (texto, palabra) {

      if(this.$refs.form.validate()){

        var a  = {};
        var b  = {};

        var auxTexto       = texto.toLowerCase();
        var auxPalabra     = palabra.toLowerCase();

        var arrayDeCadenas = auxTexto.split(' ');
        arrayDeCadenas.forEach(function(value){
          if(value == auxPalabra) {
            a[value] = (a[value] || 0) + 1;
          }else {
            b[value] = (b[value] || 0) + 1;
          }
        });
        this.countTotal = Object.values(a);
        this.countWords = b;

      }



    }
  },
}
</script>
