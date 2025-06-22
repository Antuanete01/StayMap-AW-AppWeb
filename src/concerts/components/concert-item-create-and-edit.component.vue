<script>
import CreateAndEditComponent from "@/shared/components/create-and-edit.component.vue";

export default {
  name: "concert-item-create-and-edit-dialog",
  components: {CreateAndEditComponent},
  props: {
    item: null,
    visible: false,
    edit: false,
  },
  emits: ['cancel-requested', 'save-requested'],
  data() {
    return {
      submitted: false
    }
  },
  methods: {
    onCancelRequested() {
      this.$emit('cancel-requested');
    },
    onSaveRequested() {
      this.submitted = true;
      this.$emit('save-requested', this.item);
    }
  }
}
</script>
<template>
  <create-and-edit-component
      class="dialog-container"
      :entity="item"
      :visible="visible"
      :edit="edit"
      entity-name="Concierto"
      size="standard"
      @cancel-action-requested="onCancelRequested"
      @save-action-requested="onSaveRequested"
  >
    <template #header>
      <h2 class="header-title">Nuevo concierto</h2>
    </template>

    <template #content>
      <div class="form-content">
        <!-- Artist Name -->
        <div class="field mt-5">
          <pv-float-label>
            <label for="artistName">Artist Name</label>
            <pv-input-text
                id="artistName"
                v-model="item.artistName"
                :class="{ 'p-invalid': submitted && !item.artistName }"
            />
          </pv-float-label>
        </div>

        <!-- Artist Genre -->
        <div class="field mt-3">
          <pv-float-label>
            <label for="genre">Artist Genre*</label>
            <pv-dropdown
                id="genre"
                :options="['Pop', 'Rock', 'K-pop', 'Indie', 'Urbano', 'Electrónica', 'Salsa', 'Cumbia', 'Jazz']"
                v-model="item.genre"
                placeholder="Select a genre"
                :class="{ 'p-invalid': submitted && !item.genre }"
            />
          </pv-float-label>
        </div>

        <!-- Image URL -->
        <div class="field mt-3">
          <pv-float-label>
            <label for="image">Image URL</label>
            <pv-input-text id="image" v-model="item.image" />
          </pv-float-label>
        </div>

        <!-- Description -->
        <div class="field mt-3">
          <pv-float-label>
            <label for="description">Description</label>
            <pv-input-text id="description" v-model="item.description" />
          </pv-float-label>
        </div>

        <!-- Date -->
        <div class="field mt-3">
          <pv-float-label>
            <label for="date">Date*</label>
            <pv-calendar id="date" v-model="item.date" show-icon />
          </pv-float-label>
        </div>

        <!-- Venue Name -->
        <div class="field mt-3">
          <pv-float-label>
            <label for="venueName">Venue's name</label>
            <pv-input-text id="venueName" v-model="item.venueName" />
          </pv-float-label>
        </div>

        <!-- Venue Address -->
        <div class="field mt-3">
          <pv-float-label>
            <label for="venueAddress">Venue's address</label>
            <pv-input-text id="venueAddress" v-model="item.venueAddress" />
          </pv-float-label>
        </div>
      </div>
    </template>
  </create-and-edit-component>
</template>
<style >
.dialog-container {
  background-color: #000000;
  padding: 2rem;
  border-radius: 20px;
  color: white;
}

.header-title {
  color: #cb6ce6;
  text-align: center;
  width: 100%;
  font-size: 1.5rem;
  font-weight: bold;
  margin: 0 auto;
}

.form-content {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  padding-top: 1rem;
}

.field {
  display: flex;
  flex-direction: column;
}

label {
  color: #cb6ce6;
  font-weight: 600;
  margin-bottom: 5px;
}

input,
.p-inputtext {
  border-radius: 12px;
  padding: 10px;
  background-color: #2a2a2a;
  border: 1px solid #cb6ce6;
  color: white;
}

input::placeholder,
.p-inputtext::placeholder {
  color: #bbb;
}

input:focus,
.p-inputtext:focus {
  border-color: #cb6ce6;
  box-shadow: 0 0 5px #cb6ce6;
}
</style>