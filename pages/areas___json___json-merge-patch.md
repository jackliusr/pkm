- ``` python
   define MergePatch(Target, Patch):
         if Patch is an Object:
           if Target is not an Object:
         		Target = {} # Ignore the contents and set it to an empty Object
              
           for each Name/Value pair in Patch:
         		if Value is null:
                 if Name exists in Target:
                   remove the Name/Value pair from Target
              else:
               Target[Name] = MergePatch(Target[Name], Value)
              
            return Target
         else:
           return Patch
  ```