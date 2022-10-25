<template>
  <div class="jumbotron">
    <vue-form :state="formState" @submit.prevent="send()">
      <validate tag="div">
        <br>
      <br>
      
        <label for="Nombre" style="font-size: 48px;">Nombre</label>
        <input
          class="form-control"
          type="text"
          id="Nombre"
          name="Nombre"
          v-model.trim="formData.Nombre"
          autocomplete="off"
          :minlength="minNombreLength"
          :maxlength="maxNombreLength"
          required
        />
        <field-messages name="Nombre" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>
          <div slot="minlength" class="alert alert-danger mt-1">
            Este campo requiere {{ minNombreLength }} caracteres como mínimo
          </div>
          <div
            v-if="formData.Nombre.length === maxNombreLength"
            class="alert alert-warning mt-1"
          >
            Máximo {{ maxnameLength }} caracteres
          </div>
        </field-messages>
      </validate>
      <br>
      <br>
      <validate tag="div">
        <label for="age" style="font-size: 48px;">Edad</label>
        <input
          class="form-control"
          type="number"
          id="Edad"
          :min="minEdad"
          :max="maxEdad"
          name="Edad"
          v-model.number="formData.Edad"
          autocomplete="off"
          required
        />
        <field-messages name="Edad" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>
          <div slot="min" class="alert alert-danger mt-1">
            Edad mínima: {{ minEdad }} años
          </div>
          <div slot="max" class="alert alert-danger mt-1">
            Edad máxima: {{ maxEdad }} años
          </div>
        </field-messages>
      </validate>
      <br>
      <br>
      <validate tag="div">
        <label for="email" style="font-size: 48px;"> E-mail</label>
        <input
          class="form-control"
          type="email"
          id="email"
          name="email"
          v-model.trim="formData.email"
          autocomplete="off"
          required
        />
        <field-messages name="email" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>
          <div slot="email" class="alert alert-danger mt-1">
            Email no válido
          </div>
        </field-messages>
      </validate>
      <br>
      <br>
      <button
        class="btn btn-success my-3"
        :disabled="formState.$invalid"
        type="submit" style="font-size: 32px;"
      >
        Enviar
      </button>
    </vue-form>
    <br>
      <br>
    <div class="table-responsive">
      <table class="table table-light" style="font-size: 32px; font-style: italic;">
        <tr>
          <th v-for="(col, i) in getColumnas" :key="i">{{ col }}</th>
        </tr>
        <td v-for="(v, i) in formData" :key="i">
          {{ v }}
        </td>
      </table>
    </div>
  </div>
</template>

<script lang="js">
export default {
  name: 'src-components-form',
  props: [],
  mounted() {
  },
  data() {
    return {
      formData: this.getFormInicial(),
      formState: {},
      minNombreLength: 5,
      maxNombreLength: 15,
      minEdad: 18,
      maxEdad: 120
    }
  },
  methods: {
    getFormInicial() {
      return {
        Nombre: '',
        Edad: '',
        email: ''
      }
    },
    send() {
      this.formData = this.getFormInicial()
       this.formState._reset()
    },
  },
  computed: {
    getColumnas() {
      return Object.keys(this.formData)
    }
  }
}
</script>

<style>
.jumbotron {
    color: black;
    /* background-color:darkgrey; */
    text-align: center;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

.table-responsive{
  color: black;
}
</style>
 