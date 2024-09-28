<template>
  <div class="container py-10">
    <div class="overflow-x-auto rounded-md border pb-3">
      <UiTable>
        <UiTableCaption>A list of registered users.</UiTableCaption>
        <UiTableHeader>
          <UiTableRow>
            <UiTableHead>First name</UiTableHead>
            <UiTableHead>Last name</UiTableHead>
            <UiTableHead>Email</UiTableHead>
            <UiTableHead>Username</UiTableHead>
            <UiTableHead class="text-right">Actions</UiTableHead>
          </UiTableRow>
        </UiTableHeader>
        <UiTableBody class="last:border-b">
          <template v-for="usr in demoUsers" :key="usr.id">
            <UiTableRow>
              <UiTableCell class="font-medium">{{ usr.firstName }}</UiTableCell>
              <UiTableCell>{{ usr.lastName }}</UiTableCell>
              <UiTableCell>{{ usr.email }}</UiTableCell>
              <UiTableCell>
                {{ usr.username }}
              </UiTableCell>
              <UiTableCell class="text-right">
                <!-- Set the record that should be manipulated from the button click -->
                <UiButton
                  @click="
                    editItem = usr;
                    model = true;
                  "
                  variant="outline"
                  size="icon"
                  ><Icon class="h-4 w-4" name="material-symbols:person-remove"
                /></UiButton>
              </UiTableCell>
            </UiTableRow>
          </template>
        </UiTableBody>
      </UiTable>
    </div>
    <!-- Move the dialog outside the table -->
    <!-- This way performance is better -->
    <UiAlertDialog v-model:open="model">
      <UiAlertDialogContent>
        <UiAlertDialogHeader>
          <UiAlertDialogTitle>Are you absolutely sure?</UiAlertDialogTitle>
          <UiAlertDialogDescription
            >This action cannot be undone. This will permanently remove the user from the
            application</UiAlertDialogDescription
          >
        </UiAlertDialogHeader>
        <UiAlertDialogFooter>
          <!-- Clear the record to be edited if the user decides to cancel -->
          <UiAlertDialogCancel @click="editItem = undefined" />
          <UiAlertDialogAction @click="handleRemove" />
        </UiAlertDialogFooter>
      </UiAlertDialogContent>
    </UiAlertDialog>
  </div>
</template>
<script lang="ts" setup>
  const model = ref(false);
  // Use a ref to store the record that should be manipulated
  const editItem = ref();
  // I think it's better to use a reactive object instead of an array
  const demoUsers = ref([
    {
      id: "691e66bf-ef80-4611-96df-a2c96dc8e18c",
      firstName: "admin",
      lastName: "admin",
      email: "admin@test.com",
      username: "admin",
    },
    {
      id: "f73c17cf-52b7-4406-a6d0-3b278f5ae0d6",
      firstName: "test",
      lastName: "test",
      email: "test@test.com",
      username: "test",
    },
    {
      id: "ab7c26dc-66b0-401e-b504-624b287c9918",
      firstName: "test2",
      lastName: "test2",
      email: "test2@test.com",
      username: "tes2t",
    },
  ]);

  const handleRemove = () => {
    // Check if the record is set
    if (!editItem.value) return;
    // Find the index of the record to be removed
    const index = demoUsers.value.findIndex((usr) => usr.id === editItem.value.id);
    // Remove the record from the array
    demoUsers.value.splice(index, 1);
    // Clear the record
    editItem.value = undefined;
  };
</script>
