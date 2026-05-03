**PRACTICE ASSIGNMENTS FOR UNIX**

**Basic Unix Commands :**

1. Create a directory Unix in your home directory

2. Create two sub directories dir1 and dir2 under Unix directory.

3. Go to dir1.

4. Create a file myFile in the dir1 and insert few lines.

5. Make a duplicate copy of the file myFile in dir2

6. Append few lines of statements in file myFile in dir2.

7. Change the name of the file myFile in dir2 to newFile.

 

**Filters and Pipes:**

Consider this file as the sample myFile.

 

Hello\!

Welcome to this course on Unix.

You are expected to complete the assignments to complete the course.

You can save this file in your system to use it. This file can be used for practice.

I have created this file to complete this assignment.

Happy Learning\!

 

8. Display how many number of lines are there in myFile.

**Expected Output :** 6

      9.Count how many users are currently logged into the system

     10.Display the lines having the word "this"/”This” in myFile

**Expected Output :**

Welcome to this course on Unix.

You can save this file in your system to use it. This file can be used for practice.

I have created this file to complete this assignment.

 

     11.Count number of lines having the word "this"/”This” in myFile.

**Expected Output : **3

 

    12.Replace the word this by that for all occurrences in myFile.

 

**Expected Output :**

Hello\!

Welcome to that course on Unix.

You are expected to complete the assignments to complete the course.

You can save that file in your system to use it. This file can be used for practice.

I have created that file to complete that assignment.

Happy Learning\!

   13.Replace the word this by that only for the first occurrence of it in a line.

**Expected Output :**

Hello\!

Welcome to that course on Unix.

You are expected to complete the assignments to complete the course.

You can save that file in your system to use it. This file can be used for practice.

I have created that file to complete this assignment.

Happy Learning\!

 

    14\. Print the first 3 lines from the file myFile

**Expected Output :**

Hello\!

Welcome to this course on Unix.

You are expected to complete the assignments to complete the course.

 

    15\. Print the last 3 lines from the file myFile

**Expected Output :**

You can save this file in your system to use it. This file can be used for practice.

I have created this file to complete this assignment.

Happy Learning\!

 

16\. Append a new line in the beginning of the file myFile

 

**awk Scripting :**

 

17. Create a file with name student.txt with the following contents in it

RollNo|Name|Marks1|Marks2|Marks3

123|Raghu|80|90|60

342|Maya|45|78|82

561|Gita|56|71|89

480|Mohan|71|90|89

 

a. Write an awk command to print the name and roll number of the students.

 

**Expected Output:**

 

Name RollNo

Raghu 123

Maya 342

Gita 561

Mohan 480

 

b . Write the awk command to calculate the total marks of each student and display the total marks along with the name of the student.

 

**Expected Output:**

 

Raghu-230

Maya-205

Gita-216

Mohan-250

 

 

**Shell Scripting**

 

18. Write a shell script to print the sum of the 1st 10 natural numbers.

 

**Expected Output: **55

 

 

19\. Write a shell script to print the odd numbers from a given list of numbers. The list of numbers will be given as command line argument.

 

**Example :**

 

If input numbers are 10,3,45,6,1,100, then

 

**Expected Output :**

 

3

45

1

 

 

      20\. Create a file studentScores.txt and append the following content to it.

RollNo|Name|Marks

123|Raghu|80

342|Maya|45

561|Gita|56

480|Mohan|71

 

write a shell script named scores.sh to find the name of the student who scored highest marks. Incorporate validations for the following :

a. Whether correct number of command line arguments are passed or not.

b. whether the given files exists or not.

c. whether the given file is readable or not.

 

**Expected Output :**

 

a. When executed as sh scores.sh, output should be

 

“Pass correct number of arguments.”

 

b. When executed as sh scores.sh studentScores.txt, but studentScores.txt does not exist, output should be

 

“ File does not exist”

 

c.When executed as sh scores.sh studentScores.txt, but studentScores.txt does not have read permission, output should be

 

“ File is not readable”.

 

d. When executed as sh scores.sh studentScores.txt, output should be

 

“Name of the student with highest marks : Raghu”

 

 

**Practice the questions in any of the below given link :**

1. [https://www.tutorialspoint.com/unix\_terminal\_online.php](https://www.tutorialspoint.com/unix_terminal_online.php)

2. [http://www.compileonline.com/execute\_bash\_online.php](http://www.compileonline.com/execute_bash_online.php)

3. [https://bellard.org/jslinux/vm.html?url=https://bellard.org/jslinux/buildroot-x86.cfg](https://bellard.org/jslinux/vm.html?url=https://bellard.org/jslinux/buildroot-x86.cfg)

 

