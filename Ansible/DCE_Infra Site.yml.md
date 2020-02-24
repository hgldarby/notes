# DCE_Infra Site.yml

### Common

#### Configure Baseline

- Run the `common` role for all the hosts

- Tag - "common"

  

#### Set up Ansible Master

- Run the `ansible` role for localhost only (host machine) 

- Tag - "master"

  

### Databases

- Deploy PostgreSQL to the central_db, regional_dce_db(all regions) and regional_fs_db(all regions)
  - `serial` - defined how many hosts Ansible should manage at a single time
  - Uses role `postgres10` 
  - Tag - "postgres10"
- Setup PostgreSQL DCE database
  - only on the regional_dce_db's
  - Uses role `postgre_dce`
  - vars file - `vars/dcedb.yml`
  - 



