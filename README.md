Download Link: https://assignmentchef.com/product/solved-assignment-1-cs448-introduction-to-information-security
<br>
INSTRUCTIONS TO STUDENTS:

<ul>

 <li>Any collaboration or assistance of any kind is strictly prohibited; all work must be your own.</li>

 <li>Your submission <em>will surely </em>be compared with the submissions for your peers for plagiarism detection (e.g., MOSS). Any academic dishonesty will be directly reported to the university.</li>

 <li>You have total five grace days in this semester.</li>

</ul>

<h1>1         True-False Questions (30 points)</h1>

<ol>

 <li>True or false: Message Authentication Code (MAC) prevents an adversary from modifying or injecting messages between two parties with a symmetric secret key; thus, it makes replay attacks ineffective. (A) True, (B) False</li>

 <li>True or false: In the Needham-Schroeder protocol, each participating party (e.g., A or B) becomes an encryption oracle to the other; i.e., provide a ciphertext for a plaintext chosen by another party. (A) True, (B) False</li>

 <li>True or false: All entity authentication protocols require on-line (i.e., always on, always accessible) trusted third parties.</li>

</ol>

(A) True, (B) False

<ol start="4">

 <li>True or false: The Diffie-Hellman key exchange protocol needs a trusted third party to determine the group parameters used for shared-secret generation.</li>

</ol>

(A) True, (B) False

<ol start="5">

 <li>True or false: Whenever <em>n </em>= <em>p</em><em>q</em>, where <em>p </em>and <em>q </em>are distinct primes, finding Euler’s totient function of n, denoted by <em>φ</em>(<em>n</em>), allows finding secret key <em>d </em>efficiently (i.e., in polynomial time in the length of <em>n</em>). (A) True, (B) False</li>

 <li>True or false: A hash function that is second pre-image resistant is not necessarily pre-image resistant. (A) True, (B) False</li>

</ol>

<strong>1.1       Submission</strong>

<strong>Submission. </strong>Write a text file p1S #<em>.</em>txt, where # denotes your student id. In the text file, write your answer letters (i.e., A or B) for six questions and use newline to separate them. For example,

1

<strong>Assignment 1                                                                                                                                       CS448</strong>

In p1_S_20210001.txt file:

A

B

A

B

A

B

Include this text file into the final tar file of your padding oracle attack; see the next section.

<h1>2         Padding Oracle Attack (70 points)</h1>

For this assignment, you will implement a padding attack discussed in class. This attack was first discussed in the paper “Security Flaws Induced by CBC Padding – Applications to SSL, IPSEC, WTLS…” by S. Vaudenay. You should read the paper (http://dx.doi.org/10.1007/3-540-46035-7_35) and implement the described attack.

You will have the opportunity to create your own padding attack discussed in class to extract a message from a ciphertext. You can find a set of valid ciphertexts on the KLMS assignment #1 handout section. The ciphertexts will be given as a 128-bit hexadecimal number (starting with 0x<em>…</em>) computed as follows:

<em>C </em>= <em>C</em><sub>0</sub>k<em>C</em><sub>1 </sub>= CBC<sup>Encrypt</sup><em><sub>K </sub></em>(PAD(<em>M</em>))<em>,                                           </em>(1)

where the word <em>M </em>is shorter than or equal to 8 ASCII characters (i.e., 64 bits). The block size of the cipher and the length of the secret key <em>K </em>are 64 bits. The first 64-bit block of <em>C </em>is the initialization vector (IV), which we denote <em>C</em><sub>0</sub>, and the last 64-bit block is the first cipher block, <em>C</em><sub>1</sub>. Note that we assume the randomized CBC encryption; that is, the IV (<em>C</em><sub>0</sub>) is randomly selected for every message.

You are given a <em>padding oracle</em>, which can be accessed by function calls; see Section 2.2 for the details. You can access the padding oracle as many times as you want. You will have two language options to develop your padding attack program: Java or Python. The padding oracle will accept both <em>C</em><sub>0 </sub>and <em>C</em><sub>1 </sub>(each 64 bits long), and return a 1 or a 0, indicating correct or incorrect padding respectively. The padding oracle works as follows:

{0<em>,</em>1} = CheckPAD(CBC<sup>Decrypt</sup><em><sub>K </sub></em>(<em>C</em>))<em>,                                         </em>(2)

where you provide the <em>C</em>; i.e., you are a chosen-ciphertext attacker.

<strong>2.1          Where to obtain the ciphertext?</strong>

KLMS assignment #1.

<strong>2.2         How to access the oracle?</strong>

You will be given the following list of files:

<ul>

 <li>pad oracle.jar: Padding oracle (Java bytecode).</li>

 <li>oracle python v1 2.py: Padding and decryption oracles (Python functions).</li>

 <li>python interface v1 2.jar: Java bytecode for interfacing Python scripts and oracle Java bytecodes.</li>

 <li>bcprov-jdk15-130.jar: Crypto library.</li>

</ul>

We recommend these versions for your assignment: Java 11, Python 3.6.

Here are the example codes that access the oracles. Java:

2

<strong>Assignment 1                                                                                                                                       CS448</strong>

// query padding oracle pad_oracle p = new pad_oracle ();

boolean isPaddingCorrect = p.doOracle(“0x1234567890abcdef”, “0x1234567890abcdef”);

Python:

Execute the Java-Python interface class by

java -cp pad_oracle.jar:bcprov-jdk15-130.jar:python_interface_v1_2.jar python_interface_v1_2 In your Python script, from oracle_python_v1_2 import pad_oracle

# query padding oracle

ret_pad = pad_oracle(’0x1234567890abcdef’, ’0x1234567890abcdef’);

<strong>2.3        Submission and grading</strong>

<strong>Submission. </strong>Your code has name p2S #<em>.</em>java (or <em>.</em>py) where # denotes your student id. Tar all your codes and your True-False answer p1S #<em>.</em>txt (S #<em>.</em>tar) and upload it to KLMS assignment #1. Your code should accept two command-line arguments <em>C</em><sub>0 </sub>and <em>C</em><sub>1 </sub>in the following format:

For java

<ul>

 <li>javac -cp pad oracle.jar p2 S #.java</li>

 <li>java -cp pad oracle.jar:bcprov-jdk15-130.jar: p2 S # <em>C</em><sub>0 </sub><em>C</em><sub>1</sub></li>

</ul>

For python

<ul>

 <li>python p2 S #.py <em>C</em><sub>0 </sub><em>C</em><sub>1</sub></li>

</ul>

The ciphertext blocks (<em>C</em><sub>0 </sub>and <em>C</em><sub>1</sub>) have hex format starting with 0x. The output must be the plaintext in ASCII format.

<strong>Grading. </strong>Your code should successfully obtain the plaintext from a ciphertext. You will get 40 pts if your code works for the ciphertexts that are available on handouts. If it works with all the other ciphertexts (not given to students), an additional 30 pts will be given.

3