## Terminal CLI

  

Command-line commands with [Codecademy tutorial](https://www.codecademy.com/article/command-line-commands)

```shell
#Directories
>> cd                                           #Take argument as directory string
>> cd ..                                        #Move up
>> cd /                                         #Root
>> mkdir <new-folder-name>                      #Make directory
>> ls                                           #List files in the working directory
>> ls -a                                        #List all files including hidden
>> 
#Files
>> mv <target-file.ext> <dest-folder-name>/     #Moves file to destination
>> cp <target-file.ext> <dest-folder-name>/     #Copies file to destination
>> cp * <dest-folder-name>/                     #Copies all files
>> cp *.txt <dest-folder-name>                  #Copies all .txt files
>> cp dog*.png  <dest-folder-name>              #Copies all .img files starting with "dog"
>> touch <file-name>.<extention>                #Creates a file

#Standard Inputs
>> <fileA.txt> >  <fileB.txt>                   #Redirects command on the left to the right file
>> <fileA.txt> >> <fileB.txt>                   #Appends the left file to the right file
>> <fileA.txt> <  <fileB.txt>                   #Inputs the file on the right into the left
```