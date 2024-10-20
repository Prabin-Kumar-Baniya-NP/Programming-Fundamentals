# String

## Substring and Subsequence in a String

- A substring is a contiguous sequence of characters within a string.
- Unlike substrings, subsequences do not require the characters to be contiguous.

```
Original string: "abcdef"
Substrings: "abc", "bcd", "cde", "def", "a", "ab", "bc", etc.
Subsequences: "ace", "abc", "abf", "bdf", "a", "ab", "bc", "def", etc.
```

### Get all substrings of the given string

```py
def get_substring(string):
    sub_string = []
    for i in range(0, len(string)):
        for j in range(i+1, len(string)+1):
            sub_string.append(string[i:j])
    return sub_string

print(get_substring("abcd"))
```

### Get all sub-sequence of the given string

- There are (2^n) subsequences for a string of length (n).

```py
def get_subsequence(string, index=0, new_string="", result=set()):
    if (index == len(string)):
        result.add(new_string)
        return

    current_character = string[index]
    # Include
    get_subsequence(string, index+1, new_string + current_character)
    # Exclude
    get_subsequence(string, index+1, new_string, result)
    return result


print(get_subsequence("abc"))
```

### Pattern Matching from a given text

```py
text = "THIS IS A TEST TEXT TEST TEST TEST"
pat = "TEST"
index = []
i = 0

for j in range(0, len(text)):
    current_char = text[j]
    if current_char == pat[i]:
        i += 1
    else:
        i = 0
    if (i == len(pat)):
        index.append(j - (len(pat) -1))
        i=0

print(index)
```

### WildCard Pattern Matching from a given text

```py
text = "baaabab"
pat = "*****ba*****ab"
sub_patterns = []
for item in pat.split("*"):
    if item != "":
        sub_patterns.append(item)

i = 0
j = 0
for k in range(0, len(text)):
    if text[k] == sub_patterns[j][i]:
        i += 1
    else:
        i = 0
    
    if i == len(sub_patterns[j]):
        j += 1
        i = 0
    
if j == len(sub_patterns):
    print(True)
else:
    print(False)
```

## Reverse the String

### Reverse String using Iterative approach

```py
text = "python"
reverse = ""
n = len(text)

while (n != 0):
    reverse = reverse + text[n-1]
    n -= 1

print(reverse)
```

### Reverse String using Recursive Approach

```py
text = "python"

def reverse_string(text):
    if len(text) == 0:
        return text
    current_char = text[0]
    new_string = reverse_string(text[1:])
    return new_string + current_char

print(reverse_string(text))
```

## Binary String

### Find i’th Index character in a binary string obtained after n iterations
```
Given a decimal number m, convert it into a binary string and apply n iterations. 
In each iteration, 0 becomes “01” and 1 becomes “10”. 
Find the (based on indexing) index character in the string after the nth iteration.

Examples:  

Input : m = 5, n = 2, i = 3
Output : 1
Input : m = 3, n = 3, i = 6
Output : 1
```
```
def decimal_to_binary(num):
    if num == 0:
        return "0"
    
    binary = ""
    while num > 0:
        binary = str(num % 2) + binary
        num //= 2
    return binary

def next_binary_num_str(char):
    if char == "0":
        return "01"
    elif char == "1":
        return "10"

def apply_iterations(binary_str, n):
    for _ in range(n):
        new_binary_str = ""
        for char in binary_str:
            new_binary_str += next_binary_num_str(char)
        binary_str = new_binary_str
    return binary_str

def find_kth_character(m, n, k):
    binary_str = decimal_to_binary(m)
    final_str = apply_iterations(binary_str, n)
    return final_str[k - 1]  # Adjust for 1-based indexing

# Example usage
m = 5
n = 2
k = 5
result = find_kth_character(m, n, k)
print(result)  # Output: 0

```
### Generate Binary String

```
Given an integer, K. Generate all binary strings of size k without consecutive 1’s.

Examples: 

Input : K = 3  
Output : 000 , 001 , 010 , 100 , 101 
Input : K  = 4 
Output :0000 0001 0010 0100 0101 1000 1001 1010
```
```py
def generate_binary_string(binary, k, result):
    if len(binary) == k:
        if not "11" in binary:
            result.append(binary)
        return result
    
    generate_binary_string(binary + '0', k, result)
    generate_binary_string(binary + '1', k, result)
    return result

total_binary_string = generate_binary_string("0", 3, [])
total_binary_string.extend(generate_binary_string("1", 3, []))
print(total_binary_string)
```