# Bandit OverTheWire Writeup (Levels 1-20) 🚀

## Introduction 📖
The Bandit wargame from OverTheWire is a great way to learn Linux commands and basic cybersecurity concepts. This writeup provides solutions for levels for beginners.
## Connecting to Bandit 🔗
Each level requires an SSH connection using the provided credentials.
```sh
kali@kali:~$ ssh banditX@bandit.labs.overthewire.org -p 2220
```
Replace `X` with the current level number and enter the retrieved password when prompted.

---

## **Solutions** ✅

### **Level 0 → Level 1**
#### **Task:** 📜
Retrieve the password stored in the file `readme` in the home directory.

#### **Solution:** 🏆
```sh
cat readme
```
Copy the displayed password and use it to log in to Level 1.

---

### **Level 1 → Level 2**
#### **Task:** 🔎
Find the password stored in the `-` file.

#### **Solution:** 🎯
```sh
cat ./-
```

---

### **Level 2 → Level 3**
#### **Task:** 🔍
Find the password inside the `spaces in this filename` file.

#### **Solution:** 📝
```sh
cat "spaces in this filename"
```

---

### **Level 3 → Level 4**
#### **Task:** 🕵️‍♂️
Find the password inside a hidden file located in the `inhere` directory.

#### **Solution:** 🔦
```sh
ls -a inhere
cat inhere/.hidden
```

---

### **Level 4 → Level 5**
#### **Task:** 🧐
Find the password inside a file with human-readable content in `inhere`.

#### **Solution:** 📂
```sh
file inhere/*
cat inhere/-file07
```

---

### **Level 5 → Level 6**
#### **Task:** 🎭
Find the password in a file owned by `bandit6`, with a size of 1033 bytes.

#### **Solution:** 🔑
```sh
find / -user bandit6 -size 1033c 2>/dev/null
cat /var/lib/dpkg/info/bandit6.password
```

---

### **Level 6 → Level 7**
#### **Task:** 🔍
Find the password stored in a file somewhere in `/` with the word "millionth".

#### **Solution:** 💡
```sh
find / -type f -exec grep -l "millionth" {} 2>/dev/null \;
cat /var/lib/dpkg/info/bandit7.password
```

---

### **Level 7 → Level 8**
#### **Task:** 📝
Find the password in a file containing only ASCII text and stored in `data.txt`.

#### **Solution:** 🔢
```sh
grep "millionth" data.txt
```

---

### **Level 8 → Level 9**
#### **Task:** 🧐
Find the password in `data.txt` that appears only once.

#### **Solution:** 🎯
```sh
sort data.txt | uniq -u
```

---

### **Level 9 → Level 10**
#### **Task:** 🔠
Find the password in `data.txt`, which is base64 encoded.

#### **Solution:** 🔓
```sh
base64 -d data.txt
```

---

### **Level 10 → Level 11**
#### **Task:** 🔁
Find the password in `data.txt`, which is encoded with ROT13.

#### **Solution:** 🔄
```sh
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

---

### **Level 11 → Level 12**
#### **Task:** 📦
Find the password in `data.txt`, which is a compressed file.

#### **Solution:** 🗂️
```sh
mkdir /tmp/bandit
cp data.txt /tmp/bandit/
cd /tmp/bandit
xxd -r data.txt > output.gz
gzip -d output.gz
tar -xvf output
tar -xvf output2
tar -xvf output3
tar -xvf output4
cat final_file
```

---

### **Level 12 → Level 13**
#### **Task:** 🔍
Find the password inside a hexdump file.

#### **Solution:** 💻
```sh
xxd -r data.txt > output
cat output
```

---

### **Level 13 → Level 14**
#### **Task:** 📡
Send the password via `nc` to retrieve the next password.

#### **Solution:** 📡
```sh
nc localhost 30000
Enter password
```

---

### **Level 14 → Level 15**
#### **Task:** 🔐
Same as before, but use SSL.

#### **Solution:** 🔒
```sh
openssl s_client -connect localhost:30001
Enter password
```

---

### **Level 15 → Level 16**
#### **Task:** 🗝️
Find the private SSH key and log in to Level 16.

#### **Solution:** 🎟️
```sh
cat sshkey.private > ~/.ssh/bandit16
chmod 600 ~/.ssh/bandit16
ssh -i ~/.ssh/bandit16 bandit16@localhost -p 2220
```

---

### **Level 16 → Level 17**
#### **Task:** 📡
Find the reachable port and retrieve the password.

#### **Solution:** 🌐
```sh
nmap -p- localhost
nc localhost PORT_NUMBER
```

---

### **Level 17 → Level 18**
#### **Task:** 🕵️
Find a file owned by `bandit18` and execute it.

#### **Solution:** 🏆
```sh
ls -l /home/bandit17/
./passwordfile
```

---

### **Level 18 → Level 19**
#### **Task:** 🏴‍☠️
Switch user without knowing the password.

#### **Solution:** 🎭
```sh
./bandit18/bin/setuid
```

---

### **Level 19 → Level 20**
#### **Task:** 🎬
Find the password in a script that prints the password when executed.

#### **Solution:** 🚀
```sh
./bandit19/script
```

---

## Conclusion 🏁
By completing these levels, you gain a solid understanding of Linux commands, file handling, and security principles. Keep practicing and continue to explore cybersecurity challenges! 🔥
