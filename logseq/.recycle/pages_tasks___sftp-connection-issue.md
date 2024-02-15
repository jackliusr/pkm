- TODO RE: Issue connecting to SFTP server sftp8822.ntuc.org.sg with the UCEM batch job
- ``` bash
  #check if passphases are correct
  cat pass.txt | \
    sed -e 's/\([a-z_]*\)[[:space:]]*\([[:alnum:]]*\)[[:space:]]*\(.*\)$/ssh-keygen -y -P "\3" -f \1/' |\
    sh
  ```
- awk script to generate expect script for pk
  
  ``` awk
  {
   print "spawn sftp -i " $1  " -P 8823  -o LogLevel=error " $1 "@sftp8823.ntuc.org.sg"
   printf "expect \"Enter passphrase for key '%s':\"\n", $1
   printf "send -- \"%s\\r\"\n", $3
   printf "expect \"sftp>\"\n"
   print "send -- ls\\r"
   printf "expect \"sftp>\"\n"
   print "send -- bye\\r"
   print  "\n"
  }
  ```
- awk script to generate expect script for pass
  
  ``` awk
  {
   print "spawn sftp "  " -P 8823  -o LogLevel=error " $1 "@sftp8823.ntuc.org.sg"
   printf "expect \"Enter password:\"\n"
   printf "send -- \"%s\\r\"\n", $2
   printf "expect \"sftp>\"\n"
   print "send -- ls\\r"
   printf "expect \"sftp>\"\n"
   print "send -- bye\\r"
   print  "\n"
  }
  ```
- run awk script
  
  ``` bash
  cat pass.txt | awk -F"\t" -f gen.awk  > test.exp
  ```
- run expect script
  
  ``` bash
  #add shellbang
  #!/usr/bin/expect 
  #set timeout 3
  chmod +x test.exp
  ./test.exp
  ```