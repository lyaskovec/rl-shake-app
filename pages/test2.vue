<template>
  <div id="app-container">
    <DxDataGrid ... >
      <!-- ... -->
      <DxColumn data-field="FullName">
        <DxRequiredRule />
      </DxColumn>
      <DxColumn data-field="Position">
        <DxRequiredRule />
      </DxColumn>
      <DxColumn ...
                data-field="BirthDate">
        <DxRequiredRule />
      </DxColumn>
      <DxColumn ...
                data-field="HireDate">
        <DxRequiredRule />
      </DxColumn>
      <!-- ... -->
      <DxColumn ...
                data-field="Country">
        <DxRequiredRule />
      </DxColumn>
      <DxEditing
        mode="popup"
        :allow-updating="true"
        :allow-adding="true"
        :allow-deleting="true"
      />
    </DxDataGrid>
  </div>
</template>

<script>
import {
  DxDataGrid,
  DxColumn,
  // ...
  DxRequiredRule,
  DxEditing
} from 'devextreme-vue/data-grid';

export default {
  components: {
    DxDataGrid,
    DxColumn,
    // ...
    DxRequiredRule,
    DxEditing
  },
  // ...
}
</script>
