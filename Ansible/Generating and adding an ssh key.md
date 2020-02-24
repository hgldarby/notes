### Generating and adding an ssh key

- PuTTYgen - Used to create a ssh-rsa key
  - Click 'Generate' - creates a public/private key pair
  - Save the generated keys
- Pageant - A list of the used keys
  - Click 'Add Key' - select the public key you wish to add
- in dce_infra checkout:
  - need to add the public key to common.yml as well as name so that when connecting to a new vm, the key is sent automatically to each for authentication.
- https://dce.dematic.com/fossil/dce_trunk/wiki?name=SSH+Keys

