# DCE_Infra (my version)

### Inventory

- Create an inventory with the relevant virtual machines/servers you want in. Mine looks like this with only control, dce_central, dce_central_db, and dce_foss

  ```
  [control]
  control
  
  [dcecentral]
  dcecentral
  
  [dcecentraldb]
  dcecentraldb
  
  [dcefoss]
  dcefoss
  ```

- I've added headers/group names for each so each individual can be accessed using a tag in the command associated with the group name