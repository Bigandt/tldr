# .bashrc file

````
encall() {
  for i in $(find -maxdepth 1 -name "*" -type f) ; 
  do 
    encfile $i; 
  done
}

decall() {
  for i in $(find -maxdepth 1 -name "*.asc" -type f) ; 
  do 
     decfile $i; 
  done
}

encfile() {
  if [ -z "$1" ]
  then
    echo "No input argument"
    return
  fi
  gpg --encrypt --sign --armor -r jeppebigandt@gmail.com --always-trust $1
  rm $1	
}

decfile() {
  if [ -z "$1" ]
  then
    echo "No input argument"
    return
  fi
  gpg --decrypt $1 > ${1::-4}
  rm $1
}

# 1st argument has to be a file name. The file will be copied into clipboard
function xclipx(){
   xclip -sel clip < "$1"  
}
export -f xclipx

# 1st argument has to be a file name. The content of the clipbord will be written into the fi
function xclipfile(){
   xclip -o > "$1"  
}
export -f xclipfile

````