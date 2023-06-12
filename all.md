
Practical: -1
AIM: Implement RSA algorithm.
Code:
import java.io.*;
import java.math.*;
import java.util.*;
public class GCD
{
 public static double gcd(double a, double h)
{
 double temp;
while (true) 
{
 temp = a % h;
if (temp == 0)
return h;
a = h;
h = temp;
}
}
public static void main(String[] args)
{
double p = 17;
double q = 11;
 double n = p * q;
 double e = 7;
double phi = (p - 1) * (q - 1);
while (e < phi) 
 {
if (gcd(e, phi) == 1)
break;
else
e++;
}
int k = 2;
double d = (1 + (k * phi)) / e;
 double msg = 88;
 System.out.println("Message data = " + msg);
 double c = Math.pow(msg, e);
c = c % n;
System.out.println("Encrypted data = " + c);
double m = Math.pow(c, d);
m = m % n;
System.out.println("Original Message Sent = " + m);
}}
Output:



Practical: -2
AIM: Implement Playfair cipher.
Code:
import java.util.*;
public class Practical1 {
 static String removeDuplicate(String s) {
 int j, index = 0, len = s.length();
 char c[] = s.toCharArray();
 for (int i = 0; i < len; i++) {
 for (j = 0; j < i; j++) {
 if (c[i] == c[j])
 break;
 }
 if (i == j)
 c[index++] = c[i];
 }
 s = new String((Arrays.copyOf(c, index)));
 return s;
 }
 static String removeWhiteSpace(char[] ch, String key) {
 char[] c = key.toCharArray();
 for (int i = 0; i < c.length; i++)
 {
 for (int j = 0; j < ch.length; j++) {
 if (c[i] == ch[j])
 c[i] = ' ';
 }
 }
 key = new String(c);
 key = key.replaceAll(" ", "");
 return key;
 }
 static String makePair(String pt) {
 String s = "";
 char c = 'a';
 for (int i = 0; i < pt.length(); i++) {
 if (pt.charAt(i) == ' ')
 continue;
 else {
 c = pt.charAt(i);
 s += pt.charAt(i);
 }
 if (i < pt.length() - 1)
 if (pt.charAt(i) == pt.charAt(i + 1))
 s += "x";
 }
 if (s.length() % 2 != 0)
 s += "x";
 System.out.println(s);
 return s;

 }
 static int[] findIJ(char a, char b, char x[][]) {
 int[] y = new int[4];
 if (a == 'j')
 a = 'i';
 else if (b == 'j')
 b = 'i';
 for (int i = 0; i < 5; i++) {
 for (int j = 0; j < 5; j++) {
 if (x[i][j] == a) {
 y[0] = i;
 y[1] = j;
 } else if (x[i][j] == b) {
 y[2] = i;
 y[3] = j;
 }
 }
 }
 if (y[0] == y[2]) {
 y[1] += 1;
 y[3] += 1;
 } else if (y[1] == y[3]) {
 y[0] += 1;
 y[2] += 1;
 }
 for (int i = 0; i < 4; i++)
 y[i] %= 5;
 return y;
 }
 static String encrypt(String pt, char x[][]) {
 char ch[] = pt.toCharArray();
 int a[] = new int[4];
 for (int i = 0; i < pt.length(); i += 2) {
 if (i < pt.length() - 1) {
 a = findIJ(pt.charAt(i), pt.charAt(i + 1),
 x);
 if (a[0] == a[2]) {
 ch[i] = x[a[0]][a[1]];
 ch[i + 1] = x[a[0]][a[3]];
 } else if (a[1] == a[3]) {
 ch[i] = x[a[0]][a[1]];
 ch[i + 1] = x[a[2]][a[1]];
 } else {
 ch[i] = x[a[0]][a[3]];
 ch[i + 1] = x[a[2]][a[1]];
 }
 }
 }
 pt = new String(ch);
 return pt;
 }
 public static void main(String[] args) {
 Scanner sc = new Scanner(System.in);
 String pt = " armuhsea";
 String key = "monarchy";

 key = removeDuplicate(key);
 char[] ch = key.toCharArray();
 String st = "abcdefghiklmnopqrstuvwxyz";
 st = removeWhiteSpace(ch, st);
 char[] c = st.toCharArray();
 char[][] x = new char[5][5];
 int indexOfSt = 0, indexOfKey = 0;
 for (int i = 0; i < 5; i++) {
 for (int j = 0; j < 5; j++) {
 if (indexOfKey < key.length())
 x[i][j] = ch[indexOfKey++];
 else
 x[i][j] = c[indexOfSt++];
 }
 }
 for (int i = 0; i < 5; i++) {
 for (int j = 0; j < 5; j++)
 System.out.print(x[i][j] + " ");
 System.out.println();
 }
 pt = makePair(pt);
 pt = encrypt(pt, x);
 System.out.println(pt);
 }
}
Output:

Practical: -3
AIM: Implement Ceasar and Hill cipher.
Code:
Ceasar cipher:-
class Practical1 {
public static StringBuffer encrypt(String text, int s) {
StringBuffer result = new StringBuffer();
for (int i = 0; i < text.length(); i++) {
if (Character.isUpperCase(text.charAt(i))) {
char ch = (char) (((int) text.charAt(i) + s - 65) % 26 + 65);
result.append(ch);
} else {
char ch = (char) (((int) text.charAt(i) +
s - 97) % 26 + 97);
result.append(ch);
}
}
return result;
}
public static void main(String[] args) {
String text = " Hello";
int s = 3;
System.out.println("Text : " + text);
System.out.println("Shift : " + s);
System.out.println("Cipher: " + encrypt(text, s));
}
}
Output:
Hill cipher:-
class GFG
{
static void getKeyMatrix(String key, int keyMatrix[][])
{
int k = 0;
for (int i = 0; i < 3; i++)
{

 for (int j = 0; j < 3; j++)
{
keyMatrix[i][j] = (key.charAt(k)) % 65;
k++;
}
}
}
static void encrypt(int cipherMatrix[][],
int keyMatrix[][],
int messageVector[][])
{
int x, i, j;
for (i = 0; i < 3; i++)
{
for (j = 0; j < 1; j++)
{
cipherMatrix[i][j] = 0;
 for (x = 0; x < 3; x++)
{
cipherMatrix[i][j] +=
keyMatrix[i][x] * messageVector[x][j];
}
 cipherMatrix[i][j] = cipherMatrix[i][j] % 26;
}
}
}
static void HillCipher(String message, String key)
{
int [][]keyMatrix = new int[3][3];
getKeyMatrix(key, keyMatrix);
int [][]messageVector = new int[3][1];
for (int i = 0; i < 3; i++)
messageVector[i][0] = (message.charAt(i)) % 65;
int [][]cipherMatrix = new int[3][1];
encrypt(cipherMatrix, keyMatrix, messageVector);
String CipherText="";
for (int i = 0; i < 3; i++)
CipherText += (char)(cipherMatrix[i][0] + 65);
System.out.print(" Ciphertext:" + CipherText);
}
public static void main(String[] args)
{
String message = " pay";
String key = " sbburueqq ";
HillCipher(message, key);
}
}
Output:

Practical: -4
AIM: Implement Euclid algorithm to find GDC.
Code:
class Practical1 {
public static int gcd(int a, int b) {
if (a == 0)
return b;
return gcd(b % a, a);
}
public static void main(String[] args) {
int a = 16, b = 12, g;
g = gcd(a, b);
System.out.println("GCD(" + a + " , " + b + ") = " + g);
a = 12;
b = 4;
g = gcd(a, b);
System.out.println("GCD(" + a + " , " + b + ") = " + g);
a = 31;
b = 2;
g = gcd(a, b);
System.out.println("GCD(" + a + " , " + b + ") = " + g);
}
}
Output:

Practical: -5
AIM: Generate random number of 32 bits.
First Method: Linear congruential generator: -
class Practical1 {
static void linearCongruentialMethod(int Xo, int m, int a, int c, int[] randomNums, int 
noOfRandomNums) {
randomNums[0] = Xo;
for (int i = 1; i < noOfRandomNums; i++) {
randomNums[i] = ((randomNums[i - 1] * a) + c) % m;
}
}
public static void main(String[] args) {
int Xo = 5;
int m = 7;
int a = 3;
int c = 3;
int noOfRandomNums = 10;
int[] randomNums = new int[noOfRandomNums];
linearCongruentialMethod(Xo, m, a, c, randomNums, noOfRandomNums);
for (int i = 0; i < noOfRandomNums; i++) {
System.out.print(randomNums[i] + " ");
}
}
}
Output:

Second Method: Blum Blum Shub generator: -
import java.math.BigInteger;
public class Practical {
 public static void main(String[] args) {
 BigInteger p = new BigInteger("29989");
 BigInteger q = new BigInteger("30161");
 BigInteger n = p.multiply(q);
 BigInteger X0 = new BigInteger("12345"); // Choose a seed value
 BigInteger X = X0;
 BigInteger randomNum = BigInteger.ZERO;
 for (int i = 0; i < 32; i++) {
 X = X.multiply(X).mod(n);
 BigInteger bit = X.mod(BigInteger.valueOf(2));
 randomNum = randomNum.shiftLeft(1).add(bit);
 }
 System.out.println("Random number: " + randomNum);
 }
}
Output:

Practical: -6
AIM: Implement Euler’s totient function.
Code:
class Practical 
{
static int gcd(int a, int b)
{
if (a == 0)
return b;
return gcd(b % a, a);
}
static int phi(int n)
{
int result = 1;
for (int i = 2; i < n; i++)
if (gcd(i, n) == 1)
result++;
return result;
}
public static void main(String[] args)
{
int n;
 for (n = 1; n <= 37; n++)
System.out.println("phi(" + n + ") = " + phi(n));
}
}
Output:

Practical: -7
AIM: Write a program that increases file size by 10.
Code:
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;
public class FileShortcutCreator {
 public static void main(String[] args) {
 String sourceFilePath = "C:/path/to/source/file.txt";
 String shortcutFilePath = "C:/path/to/shortcut.lnk";
 
 createShortcut(sourceFilePath, shortcutFilePath);
 
 System.out.println("Shortcut created successfully.");
 }
 
 public static void createShortcut(String sourceFilePath, String shortcutFilePath) {
 try {
 Path sourcePath = Path.of(sourceFilePath);
 Path shortcutPath = Path.of(shortcutFilePath);
 
 Files.copy(sourcePath, shortcutPath, StandardCopyOption.COPY_ATTRIBUTES);
 
 // Add .lnk extension to the shortcut file if not already present
 if (!shortcutFilePath.toLowerCase().endsWith(".lnk")) {
 Path renamedShortcutPath = Path.of(shortcutFilePath + ".lnk");
 Files.move(shortcutPath, renamedShortcutPath);
 shortcutPath = renamedShortcutPath;
 }
 
 // Set the file attribute to indicate it's a shortcut
 Files.setAttribute(shortcutPath, "dos:hidden", true);
 
 } catch (Exception e) {
 System.out.println("An error occurred while creating the shortcut: " + e.getMessage());
 }
 }
}
Output:
Practical: -8
AIM: Write a program that increases file size by 10.
Code:
import java.io.*;
public class Practical {
 public static void main(String[] args) {
 String fileName = "file.txt";
 long desiredSize = 10 * 1024; // 10 KB
 try (RandomAccessFile file = new RandomAccessFile(fileName, "rw")) {
 long currentSize = file.length();
 if (currentSize < desiredSize) {
 file.seek(currentSize); // Seek to the end of the file
 while (file.length() < desiredSize) {
 file.write(0); // Write zero to increase the file size
 }
 System.out.println("File size increased to " + desiredSize + " bytes.");
 } else {
 System.out.println("File size is already greater than or equal to " + desiredSize + " 
bytes.");
 }
 } catch (IOException e) {
 System.out.println("An error occurred: " + e.getMessage());
 }
 }
}
Output:

Practical: -9
AIM: Implement rail fence and transposition cipher.
Rail Fence cipher:-
Code:
public class Practical {
 // Rail Fence Cipher
 public static String railFenceEncrypt(String plaintext, int rails) {
 StringBuilder ciphertext = new StringBuilder();
 StringBuilder[] fence = new StringBuilder[rails];
 for (int i = 0; i < rails; i++) {
 fence[i] = new StringBuilder();
 }
 int rail = 0;
 boolean directionDown = true;
 for (int i = 0; i < plaintext.length(); i++) {
 fence[rail].append(plaintext.charAt(i));
 if (rail == 0) {
 directionDown = true;
 } else if (rail == rails - 1) {
 directionDown = false;
 }
 if (directionDown) {
 rail++;
 } else {
 rail--;
 }
 }
 for (int i = 0; i < rails; i++) {
 ciphertext.append(fence[i]);
 }
 return ciphertext.toString();
 }
 public static String railFenceDecrypt(String ciphertext, int rails) {
 StringBuilder plaintext = new StringBuilder();
 StringBuilder[] fence = new StringBuilder[rails];
 int[] fenceLengths = new int[rails];
 for (int i = 0; i < rails; i++) {
 fence[i] = new StringBuilder();
 }
 int rail = 0;
 boolean directionDown = true;
 for (int i = 0; i < ciphertext.length(); i++) {
 fenceLengths[rail]++;
 if (rail == 0) {
 directionDown = true;
 } else if (rail == rails - 1) {
 directionDown = false;
 }
 if (directionDown) {
 rail++;
 } else {

 rail--;
 }
 }
 int currentIndex = 0;
 for (int i = 0; i < rails; i++) {
 fence[i].append(ciphertext, currentIndex, currentIndex + fenceLengths[i]);
 currentIndex += fenceLengths[i];
 }
 rail = 0;
 directionDown = true;
 for (int i = 0; i < ciphertext.length(); i++) {
 plaintext.append(fence[rail].charAt(0));
 fence[rail].deleteCharAt(0);
 if (rail == 0) {
 directionDown = true;
 } else if (rail == rails - 1) {
 directionDown = false;
 }
 if (directionDown) {
 rail++;
 } else {
 rail--;
 }
 }
 return plaintext.toString();
 }
 // Transposition Cipher
 public static String transpositionEncrypt(String plaintext, String key) {
 int keyLength = key.length();
 int plaintextLength = plaintext.length();
 int numRows = (int) Math.ceil((double) plaintextLength / keyLength);
 int numCols = keyLength;
 char[][] grid = new char[numRows][numCols];
 int plaintextIndex = 0;
 for (int col = 0; col < numCols; col++) {
 int keyIndex = key.indexOf(col + 1);
 for (int row = 0; row < numRows; row++) {
 if (plaintextIndex < plaintextLength) {
 grid[row][keyIndex] = plaintext.charAt(plaintextIndex++);
 }
 }
 }
 StringBuilder ciphertext = new StringBuilder();
 for (int row = 0; row < numRows; row++) {
 for (int col = 0; col < numCols; col++) {
 if (grid[row][col] != 0) {
 ciphertext.append(grid[row][col]);
 }
 }
 }
 return ciphertext.toString();
 }
 public static String transpositionDecrypt(String ciphertext, String key) {
 int keyLength = key.length();
 int ciphertextLength = ciphertext.length();
 int numRows = (int) Math.ceil((double) ciphertextLength / keyLength);
 int numCols = keyLength;

 char[][] grid = new char[numRows][numCols];
 int ciphertextIndex = 0;
 for (int col = 0; col < numCols; col++) {
 int keyIndex = key.indexOf(col + 1);
 for (int row = 0; row < numRows; row++) {
 if (ciphertextIndex < ciphertextLength) {
 grid[row][keyIndex] = ciphertext.charAt(ciphertextIndex++);
 }
 }
 }
 StringBuilder plaintext = new StringBuilder();
 for (int row = 0; row < numRows; row++) {
 for (int col = 0; col < numCols; col++) {
 if (grid[row][col] != 0) {
 plaintext.append(grid[row][col]);
 }
 }
 }
 return plaintext.toString();
 }
 public static void main(String[] args) {
 // Rail Fence Cipher Example
 String plaintext = "HELLO WORLD";
 int rails = 3;
 String railFenceCipher = railFenceEncrypt(plaintext, rails);
 String railFenceDecipher = railFenceDecrypt(railFenceCipher, rails);
 System.out.println("Rail Fence Cipher:");
 System.out.println("Plaintext: " + plaintext);
 System.out.println("Ciphertext: " + railFenceCipher);
 System.out.println("Deciphered: " + railFenceDecipher);
 System.out.println();
 // Transposition Cipher Example
 String key = "3142";
 String transpositionCipher = transpositionEncrypt(plaintext, key);
 String transpositionDecipher = transpositionDecrypt(transpositionCipher, key);
 System.out.println("Transposition Cipher:");
 System.out.println("Plaintext: " + plaintext);
 System.out.println("Ciphertext: " + transpositionCipher);
 System.out.println("Deciphered: " + transpositionDecipher);
 }
}
Output:

Transposition cipher: -
Code:
public class TranspositionCipher {
 public static String encrypt(String plaintext, String key) {
 int keyLength = key.length();
 int plaintextLength = plaintext.length();
 int numRows = (int) Math.ceil((double) plaintextLength / keyLength);
 char[][] grid = new char[numRows][keyLength];
 int plaintextIndex = 0;
 // Fill the grid with the plaintext characters
 for (int row = 0; row < numRows; row++) {
 for (int col = 0; col < keyLength; col++) {
 if (plaintextIndex < plaintextLength) {
 grid[row][col] = plaintext.charAt(plaintextIndex++);
 }
 }
 }
 StringBuilder ciphertext = new StringBuilder();
 // Read the columns based on the key order
 for (int i = 0; i < keyLength; i++) {
 int col = key.charAt(i) - '1';
 for (int row = 0; row < numRows; row++) {
 if (grid[row][col] != '\u0000') {
 ciphertext.append(grid[row][col]);
 }
 }
 }
 return ciphertext.toString();
 }
 public static String decrypt(String ciphertext, String key) {
 int keyLength = key.length();
 int ciphertextLength = ciphertext.length();
 int numRows = (int) Math.ceil((double) ciphertextLength / keyLength);
 char[][] grid = new char[numRows][keyLength];
 int ciphertextIndex = 0;
 // Fill the grid with the ciphertext characters
 for (int i = 0; i < keyLength; i++) {
 int col = key.charAt(i) - '1';
 for (int row = 0; row < numRows; row++) {
 if (ciphertextIndex < ciphertextLength) {
 grid[row][col] = ciphertext.charAt(ciphertextIndex++);
 }
 }
 }
 StringBuilder plaintext = new StringBuilder();
 // Read the grid row by row
 for (int row = 0; row < numRows; row++) {
 for (int col = 0; col < keyLength; col++) {
 if (grid[row][col] != '\u0000') {
 plaintext.append(grid[row][col]);
 }
 }
 }
 return plaintext.toString();
 }
 public static void main(String[] args) {
 String plaintext = "HELLO WORLD";
 String key = "3142";
 String ciphertext = encrypt(plaintext, key);
 String decryptedText = decrypt(ciphertext, key);
 System.out.println("Plaintext: " + plaintext);
 System.out.println("Ciphertext: " + ciphertext);
 System.out.println("Decrypted Text: " + decryptedText);
 }
}
Output:

