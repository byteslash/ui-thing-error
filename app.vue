<template>
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
            <UiAlertDialog v-model:open="model">
              <UiAlertDialogTrigger as-child>
                <UiButton variant="outline" size="icon"
                  ><Icon class="h-4 w-4" name="material-symbols:person-remove"
                /></UiButton>
              </UiAlertDialogTrigger>
              <UiAlertDialogContent>
                <UiAlertDialogHeader>
                  <UiAlertDialogTitle>Are you absolutely sure?</UiAlertDialogTitle>
                  <UiAlertDialogDescription
                    >This action cannot be undone. This will permanently remove the user from the
                    application</UiAlertDialogDescription
                  >
                </UiAlertDialogHeader>
                <UiAlertDialogFooter>
                  <UiAlertDialogCancel />
                  <UiAlertDialogAction @click="handleRemove(usr)" />
                </UiAlertDialogFooter>
              </UiAlertDialogContent>
            </UiAlertDialog>
          </UiTableCell>
        </UiTableRow>
      </template>
    </UiTableBody>
  </UiTable>
</template>
<script lang="ts" setup>
  const model = ref(false);
  const demoUsers = [
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
  ];

  const handleRemove = (selectedUser: any) => {
    console.log("useriD: ", selectedUser.id);
  };
</script>
