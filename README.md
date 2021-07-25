# bash-notes

## array
```bash
# get all the parameters of the script
array = ("$@")

# print all elements
echo ${array[@]}
echo ${array[*]}

# print all index
echo ${!array[@]}

# for loop print
for e in "${array[@]}";do 
  echo $e
done 
# c style 
for ((i=0;i<${#array[@]};i++));do
  echo "${array[$i]}"
done


# print 3 elements from index 1
echo "${array[@]:1:3}"
# print all elements from index 1
echo "${array[@]:1}"


# append 
array +=(23 34)
# or
array = ("${array[@]}" 23 34)

# merge 
array = ("${array1[@]}"  "${array2[@]}")

# delete element
index=10
unset array[$index]


# array insert function 
insert(){
 h='
################## insert ########################
# Usage:
# insert arr_name index element
#
# Parameters:
# arr_name : Name of the array variable
# index : Index to insert at
# element : Element to insert
##################################################
 '
 [[ $1 = -h ]] && { echo "$h" >/dev/stderr; return 1; }
 declare -n __arr__=$1 # reference to the array variable
 i=$2 # index to insert at
 el="$3" # element to insert
 # handle errors
 [[ ! "$i" =~ ^[0-9]+$ ]] && { echo "E: insert: index must be a valid integer" >/dev/stderr;
return 1; }
 (( $1 < 0 )) && { echo "E: insert: index can not be negative" >/dev/stderr; return 1; }
 # Now insert $el at $i
 __arr__=("${__arr__[@]:0:$i}" "$el" "${__arr__[@]:$i}")
}

```

## map 
```bash
# declaring an associative array before initialization
declare -A array
array["name"] = "super"
array["page"] = "next"
# single statement
array=(["name"]="super" ["page"]="next")

# print value that key is name
echo ${array["name"]}

# loop
for key in "${!array[@]}";do
  echo "key: $key"
  echo "value: ${array[$key]}"
done

# elements length
echo "${#array[@]}"

```

## string to array
```bash
string="12 13 14 15"
array=(${string// /})
string="12+13+14+15"
array=(${string//+/})
```
