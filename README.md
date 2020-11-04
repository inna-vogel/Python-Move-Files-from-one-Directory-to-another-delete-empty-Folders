# Move files with python from one folder (directory) to another
# Delete empty folders in directory


```python
# import libraries
import os
import shutil #library for copying, moving and deleting files and folders
```


```python
#Simple code for moving files from one folder to another

file_src = r"place\your\source\folder\path\here"
file_dest = r"place\your\destination\folder\path\here" 

for folder in os.listdir(file_src):
    full_path = file_src + "\\" + folder #get full path to folder
    print(full_path)    
    shutil.move(os.path.join(file_src, filename), os.path.join(file_dest, filename) #move file from source folder to
                #destination folder. Override files in destination folder if same file
    if len(os.listdir(full_path)) == 0: # Check if folder is empty
        shutil.rmtree(full_path) # delete empty folder
```

## The following code I have used for a specific usecase
###### In a folder I had several duplicate folders. First I extracted the name of the folder. The I analyzed how many duplicates I had. Then I created a dictionary with name of the folder and as valua I saved the paths to the folders I wanted to merge {gallery_name:[folder1, folder2, etc.]}. Then I selected one folder where I moved all other content from duplicate folders to. The empty folders were then deleted.


```python
path = r"path\to\folder"
```


```python
names_of_galleries = []

# Extract name of Gallery
for filename in os.listdir(path):
    split = filename.split('_')
    only_name_of_gallery = " ".join(split[0:2])
    print(only_name_of_gallery)    
    full_path = path + "\\" + filename
    names_of_galleries.append(only_name_of_gallery)
    #print(full_path)    
```


```python
#Check for duplicate folders

duplicates = [x for n, x in enumerate(names_of_galleries) if x in names_of_galleries[:n]]
print(len(duplicates))
for duplicate in duplicates:
    print(duplicate)
```


```python
# Create dictionary with name of gallery and duplicate folders {gallery_name:[folder1, folder2, etc.]}
gallery_dict = {}

for filename in os.listdir(path):
    if only_name_of_gallery in duplicates:
        full_path = path + "\\" + filename
        if only_name_of_gallery not in names_dict.keys(): #if gallery not in dict, add
            names_dict.update({only_name_of_gallery:[full_path]})
        else: #if gallery exist then add duplicate folder as value
            names_dict[only_name_of_gallery].append(full_path)
```


```python
# Select source and destination paths to move files from one directory to another
for k, v in gallery_dict.items():
    source = v[0]
    dest = v[1]
    for filename in os.listdir(source):
        if filename != "Thumbs.db":  
            shutil.move(os.path.join(source, filename), os.path.join(dest, filename)) #move .jpg files from one folder 
            #to another. If destination folder contains same file, override 
        if len(os.listdir(full_path)) == 0: # Check if folder is empty
            shutil.rmtree(full_path) # delete empty folder
```

### Done!
