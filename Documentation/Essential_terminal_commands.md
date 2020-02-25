# Essential Terminal Commands

- "cd ..\fossil-repos"  -  takes you to the fossil repos directory

- "fossil new database.fossil" - adds a new database giving password to admin

- "cd ..\Think_Python_Challenge" - takes you back to the think python challenge directory

- "fossil open D:\fossil-repos\database.fossil" - opens the database python file

- "fossil commit -m "opening commit" --allow-empty"  -  allows an empty file to be committed in fossil

- "fossil ui"  -  done before next line

- "start /B fossil ui"  -  brings up fossil webpage in background

- "start /B fossil diff -tk"  -  brings up the differences in each file in the background

- "fossil changes"  -  tells you which changes you have made in any files

- "fossil extra ."  -  tells you what has been added in the directory

- "fossil add . "  -  adds the new files if applicable to fossil

- "fossil changes"  -  shows the files that you have just added

- "fossil clean -x -n --ignore .idea" - dry run of removing the cached files 

- "fossil clean -x --ignore .idea" - removes the cached files

- "fossil commit -m "database and tests files added""  -  commits the changes that have been made to fossil

  # Merge trunk to dematic_dev

- in webui
- "fossil changes" - check out dematic_dev

- "fossil update dematic_dev" - update dematic_dev

- "fossil merge trunk" - merge changes from trunk

- "fossil status" - check to see file directories

- "fossil mv **directory**" - move file from "dev" to "dce_webui"

- "fossil addrem -n" - dry run of what has been added and removed

- "fossil commit -m "pull changes from trunk"" - pull the changes from trunk



### Using CMD for fossil changes and updates etc

- "activate dce_env" - this activates the right environment
- "D:" to select the right drive
- "dce_trunk" to select the correct fossil repo
- "fossil upd"



### Using CMD for cloning a fossil repo

- create new folder in "D:" i.e. dce_trunk
- open cmd and do "D:"
- cd "dce_trunk"
- "fossil clone https://harrydarby@dce.dematic.com/fossil/dce DCE.fossil"

