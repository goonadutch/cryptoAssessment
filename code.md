--------CAESAR CIPHER--------
import java.util.Scanner;
public class Caesar {
    public static String encrypt(String text, int s){
        StringBuffer sb = new StringBuffer();
        for(int i = 0; i < text.length(); i++){
            char current = text.charAt(i);
            if(Character.isUpperCase(current)){
                char ch = (char) (((current + s - 65)% 26) + 65);
                sb.append(ch);
            }else if(Character.isLowerCase(current)){
                char ch = (char) (((current + s - 97)% 26) +97);
                sb.append(ch);
            }else if(Character.isDigit(current)){
                char ch = (char) (((current + s - 48)% 10) + 48);
                sb.append(ch);
            }else{
                sb.append(current);
            }
        }
        return sb.toString();
    }

    public static String decrypt(String text, int s){
        StringBuffer sb = new StringBuffer();
        for(int i =0; i < text.length(); i++){
            char current = text.charAt(i);
            if(Character.isUpperCase(current)){
                char ch = (char) (((current - s - 65 + 26) % 26) + 65);
                sb.append(ch);
            }else if(Character.isLowerCase(current)){
                char ch = (char) (((current - s - 97 + 26) % 26) + 97);
                sb.append(ch);
            }else if(Character.isDigit(current)){
                char ch = (char) (((current - s - 48 + 10) % 10) + 48);
                sb.append(ch);
            }else{
                sb.append(current);
            }     
        }
        return sb.toString();
    }

    public static void main(String[] args){
        Scanner ss = new Scanner(System.in);
        
        System.out.println("Enter the text  : ");
        String text = ss.nextLine();
        System.out.println("Enter the number of places to be skipped : ");
        int n = ss.nextInt();
        String encrypt = encrypt(text, n);
        System.out.println("After encryption : "+ encrypt);
        System.out.println("After decryption : " + decrypt(encrypt, n));
        ss.close();
    }
}
---------------CAESAR ATTACK------------------------
import java.util.Scanner;

public class CipherCrypt {
    public static String decryption(String cipher, int key) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < cipher.length(); i++) {
            char currentChar = cipher.charAt(i);

            if (Character.isUpperCase(currentChar)) {
                char ch = (char) (((currentChar - key - 65 + 26) % 26) + 65);
                sb.append(ch);
            } else if (Character.isLowerCase(currentChar)) {
                char ch = (char) (((currentChar - key - 97 + 26) % 26) + 97);
                sb.append(ch);
            } else if (Character.isDigit(currentChar)) {
                char ch = (char) (((currentChar - key - 48 + 10) % 10) + 48);
                sb.append(ch);
            } else {
                sb.append(currentChar);
            }
        }
        return sb.toString();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter Cipher text: ");
        String cipher = sc.nextLine();
        System.out.println("Brute Force Decryption:");
        for (int i = 1; i <= 26; i++) {
            System.out.println("Key " + i + ": " + decryption(cipher, i));
        }
        sc.close(); // Close the scanner
    }
}

----------------AFFINE CIPHER----------

import java.util.Scanner;

public class affine {
    public static int findGCD(int a, int b){
        if(b==0){
            return a;
        }
        return findGCD(b,a%b);        
    }
    public static int findInverse(int k1, int n){
        int ans =0;
        for(int i = 1; i< n; i++){
            if((k1 * i) % n == 1){
                return i;
            }
        }
        return ans;
    }
    public static String encrypt(String text, int k1, int k2){
        StringBuffer sb = new StringBuffer();
        for(int i =0; i < text.length(); i++){
            char current = text.charAt(i);
            if(Character.isUpperCase(current)){
                char ch = (char) (((current * k1) + k2 - 65) % 26 + 65);
                sb.append(ch);
            }else if(Character.isLowerCase(current)){
                char ch = (char) (((current * k1) + k2 -97) % 26 + 97);
                sb.append(ch);
            }
            //else if(Character.isDigit(current)){
            //     char ch= (char) (((current * k1) + k2 - 48) % 10 + 48);
            //     sb.append(ch);
            // }
            else{
                sb.append(current);
            }
        }
        return sb.toString();
    }

    public static String decrypt(String text, int k1, int k2){
        StringBuffer sb = new StringBuffer();
        int k = findInverse(k1, 26);
        int n = findInverse(k1, 10);
        
        for(int i =0; i < text.length(); i++){
            char current = text.charAt(i);
            if(Character.isUpperCase(current)){
                char ch = (char) (((current - k2)* k - 65 + 26) % 26 + 65);
                sb.append(ch);
            }else if(Character.isLowerCase(current)){
                char ch = (char) (((current - k2)* k -97 + 26) % 26 + 97);
                sb.append(ch);
            }
            //else if(Character.isDigit(current)){
            //     char ch = (char) (((current - k2)* n - 48 + 10) % 10 + 48);
            //     sb.append(ch);
            //}
            else{
                sb.append(current);
            }
        }
        return sb.toString();
    }
    public static void main(String[] args){
        Scanner ss = new Scanner(System.in);
        System.out.println("Enter the text : ");
        String text = ss.nextLine();
        System.out.print("Enter the key1 : ");
        int k1 = ss.nextInt();
        System.out.print("Enter the key2 : ");
        int k2 = ss.nextInt();
        int val = findGCD(k1, 26);
        if(val!=1){
            System.out.println("Decryption cannot be done!!");
            System.exit(0);
        }
        String encrypt = encrypt(text,k1,k2);
        System.out.println("Cipher: "+encrypt);
        String decrypt = decrypt(encrypt,k1,k2);
        System.out.println("After decryption: "+decrypt);
    }
}
-------------------------AFFINE ATTACK-------------------
import java.util.Scanner;
public class AffineCrypt {
    public static int gcd(int a, int b) {
        if(b==0)
            return a;
        return gcd(b,a%b);
    }
    public static int inverse(int k1){
        int ans=0;
        for(int i=0;i<26;i++) {
            if((k1*i)%26 == 1) {
                ans = i;
                break;
            }
        }
        return ans;
    }
    public static String decryption(String text, int k1, int k2) {
        StringBuffer str = new StringBuffer();
        for(int i=0;i<text.length();i++){
            if(Character.isUpperCase(text.charAt(i))) {
                int val = ((((int)text.charAt(i)-k2)*k1-65) %26+65);
                char ch = (char)val;
                str.append(ch);
            }
            else if(Character.isDigit(text.charAt(i))) {
                int val =((((int)text.charAt(i)-k2)*k1-48) %26+48);
                char ch = (char)val;
                str.append(ch);
            }
            else {
                int val =((((int)text.charAt(i)-k2)*k1-97) %26+97);
                char ch = (char)val;
                str.append(ch);
            }
        }
        return str.toString();
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter Cipher text: ");
	String cipher = sc.nextLine();
        System.out.println("Brute Force Decryption");
	for(int i=1;i<=26;i++) {
            int k = inverse(i);
            if(k==0)
                continue;
            for(int j=1;j<=26;j++) {
                System.out.println("Key "+(i)+", "+(j)+": "+decryption(cipher,k,j));
            }
        }
}
}
---------------------HILL CIPHER -------------------------
import java.util.*;
import Jama.Matrix;

public class Hill {
   
    // GCD Function
    public static int GCD(int a, int b) {
        if (b == 0)
            return a;
        return (GCD(b, a % b));
    }
    
    // Extended Eucladian Algorithm
    public static int mul_inv(int a, int b) {
        int t1 = 0, t2 = 1, t;
        int r, q;
        while (b != 0) {
            q = a / b;
            r = a % b;
            a = b;
            b = r;
            t = t1 - q * t2;
            t1 = t2;
            t2 = t;

        }
        if (t1 < 0)
            return t1 + 26;
        return t1;
    }

    // Function for Matrix Multiplication
    static int[][] multiplyMatrix(int row1, int col1,
            int A[][], int row2,
            int col2, int B[][]) {
        int i, j, k;
        int C[][] = new int[row1][col2];
        for (i = 0; i < row1; i++) {
            for (j = 0; j < col2; j++) {
                for (k = 0; k < row2; k++)
                    C[i][j] += A[i][k] * B[k][j];
            }
        }
        return C;
    }
    
    // Function to find inverse of a matrix
    public static int[][] matInverse(double[][] mat1){
        Matrix m1 = new Matrix(mat1);
        Matrix m1i = m1.inverse();
        double[][] inverseArray = m1i.getArray();
        int[][] ansArray=new int[inverseArray.length][inverseArray[0].length];
        for(int i=0;i<inverseArray.length;i++){
            for(int j=0;j<inverseArray[i].length;j++){
                int ans=(int) (Math.round(inverseArray[i][j] * m1.det()));
                ans%=26;
                if(ans<0) ans+=26;
                ans=ans*mul_inv(26,(int)(Math.round(m1.det())));
                ans%=26;
                if(ans<0) ans+=26;
                ansArray[i][j]=ans;
            }
        }
        return ansArray;
    }
    
    // Encryption Function
    public static String Encryption(String s, String key) {
        int k = key.length();
        int n = s.length();
        int keySize = (int) Math.sqrt(k);
        int strSize;
        if (n % keySize == 0)
            strSize = n / keySize;
        else
            strSize = n / keySize + 1;
        int[][] keyMatrix = new int[(int) Math.sqrt(k)][(int) Math.sqrt(k)];
        int[][] plainText = new int[keySize][strSize];

        int index = 0;
        for (int i = 0; i < keySize; i++) {
            for (int j = 0; j < keySize; j++) {
                int temp = key.charAt(index++) - 'A';
                keyMatrix[i][j]=temp;
            }
        }
        index = 0;
        for (int i = 0; i < strSize; i++) {
            for (int j = 0; j < keySize; j++) {
                if (index < n)
                    plainText[j][i] = s.charAt(index++) - 'A';
                else
                    plainText[j][i] = '-';
            }
        }
        
        int[][] result = multiplyMatrix(keySize, keySize, keyMatrix,keySize, strSize, plainText);
        String ans = "";
        for (int i = 0; i < result[0].length; i++) {
            for (int j = 0; j < result.length; j++) {
                result[j][i] = (result[j][i] % 26) + 'A';
                ans += (char) result[j][i];
            }
        }
        return ans;
    }

    // Decryption Function
    public static String Decryption(String s, String key) {
        int k = key.length();
        int n = s.length();
        int keySize = (int) Math.sqrt(k);
        int strSize;
        if (n % keySize == 0)
            strSize = n / keySize;
        else
            strSize = n / keySize + 1;
        double[][] keyMatrix = new double[(int) Math.sqrt(k)][(int) Math.sqrt(k)];
        int[][] cipherText = new int[keySize][strSize];

        int index = 0;
        for (int i = 0; i < keySize; i++) {
            for (int j = 0; j < keySize; j++) {
                int temp=key.charAt(index++) - 'A';
                keyMatrix[i][j] = temp;
            }
        }
        index = 0;
        for (int i = 0; i < strSize; i++) {
            for (int j = 0; j < keySize; j++) {
                if (index < n)
                    cipherText[j][i] = s.charAt(index++) - 'A';
                else
                    cipherText[j][i] = '-';
            }
        }
        int[][] inv=matInverse(keyMatrix);
        
        int[][] result = multiplyMatrix(keySize, keySize,inv,keySize, strSize, cipherText  );
        
        String ans = "";
        for (int i = 0; i < result[0].length; i++) {
            for (int j = 0; j < result.length; j++) {
                result[j][i] = (result[j][i] % 26) + 'A';
                ans += (char) result[j][i];
            }
        }
        return ans;
    }
    
    public static void main(String[] args) {
        Scanner input=new Scanner(System.in);
        int choice;
        
            System.out.print("Hill Cipher:-\n 1. Encryption\n 2.Decryption\n 0.Exit \n Enter your choice: ");
            choice=input.nextInt();
            switch (choice) {
                    case 1:
                        // Get the key
                        System.out.print("Enter Key Text(In square number characters): ");
                        String key = input.next();

                        // Get the PlainText and Perform Encryption
                        System.out.print("Enter text to be encrypted: ");
                        String ans = Encryption(input.next(), key);
                        if ("".equals(ans)) {
                            System.out.println("Encryption cannot be done");
                            return;
                        } else {
                            System.out.println("Encrypted Text : " + ans);
                        }
                        break;
                    case 2:
                        // Get the key
                        System.out.print("Enter Key Text(In square number characters): ");
                        key = input.next();

                        // Get CipherText and perform Decryption
                        System.out.print("Enter text to be decrypted: ");
                        ans = Decryption(input.next(), key);
                        if ("".equals(ans)) {
                            System.out.println("Decryption cannot be done");
                        } else {
                            System.out.println("Decrypted Text: " + ans);
                        }
                        break;
                    default:
                        System.out.println("Enter a valid choice...");
                        break;
            }
    }
}
                
----------------------HILL ATTACK--------------------
import java.util.Scanner;

// Cryptanalysis Function
public class CryptAttack {
    public static String Decryption(String s,int shift){
        String ans="";
        for(char c:s.toCharArray()){
            if(Character.isUpperCase(c)){
                int t1=(c-'A'-shift)%26;
                if(t1<0) t1+=26;
                char t2=(char)(t1+'A');
                ans+=t2;
            }
            else if(Character.isLowerCase(c)){
                int t1=(c-'a'-shift)%26;
                if(t1<0) t1+=26;
                char t2=(char)(t1+'a');
                ans+=t2;
            }
            else return("");
        }
        return ans;
    }
    
    public static void main(String[] args) {
        Scanner input=new Scanner(System.in);
        System.out.print("Enter CipherText: ");
        String qn=input.next();
        System.out.println("List of all possible PlainText after Cryptanalysis of Shift Cipher");
        for(int i=1;i<=26;i++){
                String ans=Decryption(qn,i);
            if( "".equals(ans)){
                System.out.println("Decryption cannot be done");
                return;
            }else{
                System.out.println(" Plain Text for Key ="+i+": "+ans);
            }
        }
        
    }
}

-----------------------TRANSPOSITION CIPHER-------------------
import java.util.Scanner;
public class Transposition
{
    public static void Cipher(char[][] mat, int n) {
        System.out.print("Cipher: ");
        int left=0, bottom=n-1;
        int top=0, right=n-1;
        while(top<=bottom && left<=right) {
            for(int i=left;i<=right;i++) {
                System.out.print(mat[top][i]+" ");
            }
            top++;
            for(int i=top;i<=bottom;i++) {
                System.out.print(mat[i][right]+" ");
            }
            right--;
            if(top<=bottom) {
                for(int i=right;i>=left;i--) {
                    System.out.print(mat[bottom][i]+" ");
                }
                bottom--;
            }
            if(left<=right) {
                for(int i=bottom;i>=top;i--) {
                    System.out.print(mat[i][left]+" ");
                }
                left++;
            }
        }
        System.out.println();
    }
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
	System.out.print("Enter text: ");
	    String text = sc.nextLine();
	    int n = (int)Math.ceil(Math.sqrt(text.length()));
	    char[][] mat = new char[n][n];
	    int k = 0;
	    for(int i=0;i<n;i++) {
	        for(int j=0;j<n;j++) {
	            while(k<text.length()) {
	                if(text.charAt(k)!=' ') {
	                mat[i][j] = text.charAt(k);
	                k++;
	                break;
	            }
	            else {
	                mat[i][j] = ' ';
	                k++;
	                break;
	            }
	            }
	        }
	    }
	System.out.println("\nMatrix");
	    for(int i=0;i<n;i++) {
	        for(int j=0;j<n;j++) {
	System.out.print(mat[i][j]+" ");
	        }
	System.out.println();
	    }
	    Cipher(mat,n);
	}
}

------------------AES----------------

import java.util.*;
import java.io.*;

public class AES {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the Plain text to be sent");
        String pt = sc.nextLine();
        String p[][] = new String[4][4];
        int k = 0;
        System.out.println("Plain text matrix");
        for (int i = 0; i < 4; i++)  {
            for (int j = 0; j < 4; j++) {
                int t = pt.charAt(k);
                String te = Integer.toHexString(t);
                p[j][i] = te;
                k++;
            }
        }
        for (int i = 0; i < 4; i++) {
            System.out.println();
            for (int j = 0; j < 4; j++) {
                System.out.print(p[i][j] + " ");
            }
        }
        System.out.println();
        System.out.println("Enter the key");
        String s[][] = new String[4][4];
        String key = sc.nextLine();
        k = 0;
        System.out.println("Key matrix");
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                int t = key.charAt(k);
                String te = Integer.toHexString(t);
                s[j][i] = te;
                k++;
            }
        }
        for (int i = 0; i < 4; i++) {
            System.out.println();
            for (int j = 0; j < 4; j++) {
                System.out.print(s[i][j] + " ");
            }
        }
        //exor key and pt
        System.out.println();
        System.out.println("New State matrix");
        String s1[][] = new String[4][4];
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                int ss = Integer.parseInt(s[i][j], 16);
                int ps = Integer.parseInt(p[i][j], 16);
                int xor = ss ^ ps;

                s1[i][j] = Integer.toHexString(xor);
            }
        }
        for (int i = 0; i < 4; i++) {
            System.out.println();
            for (int j = 0; j < 4; j++) {
                System.out.print(s1[i][j] + " ");
            }
        }
        String sbox[][] = {{"63", "7C", "77", "7B", "F2", "6B", "6F", "C5", "30", "01", "67", "2B", "FE", "D7", "AB", "76"}, {"CA", "82", "C9", "7D", "FA", "59", "47", "F0", "AD", "D4", "A2", "AF", "9C", "A4", "72", "C0"}, {"B7", "FD", "93", "26", "36", "3F", "F7", "CC", "34", "A5", "E5", "F1", "71", "D8", "31", "15"}, {"04", "C7", "23", "C3", "18", "96", "05", "9A", "07", "12", "80", "E2", "EB", "27", "B2", "75"}, {"09", "83", "2C", "1A", "1B", "6E", "5A", "A0", "52", "3B", "D6", "B3", "29", "E3", "2F", "84"}, {"53", "D1", "00", "ED", "20", "FC", "B1", "5B", "6A", "CB", "BE", "39", "4A", "4C", " 58", "CF"}, {"D0", "EF", "AA", "FB", "43", "4D", "33", "85", "45", "F9", "02", "7F", "50", "3C", "9F", "A8"}, {"51", "A3", "40", "8F", "92", "9D", "38", "F5", "BC", "B6", "DA", "21", "10", "FF", "F3", "D2"}, {"CD", "0C", "3", "EC", "5F", "97", "44", "7", "C4", "A7", "7E", "3D", "64", "5D", "19", "73"}, {"60", "81", "4F", "DC", "22", "2A", "90", "88", "46", "EE", "B8", "14", "DE", "5E", "0B", "DB"}, {"E0", "32", "3A", "0A", "49", "06", "24", "5C", "C2", "D3", "AC", "62", "91", "95", "E4", "79"}, {"E7", "C8", "37", "6D", "8D", "D5", "4E", "A9", "6C", "56", "F4", "EA", "65", "7A", "AE", "08"}, {"BA", "78", "25", "2E", "1C", "A6", "B4", "C6", "E8", "DD", "74", "1F", "4B", "BD", "8B", "8A"}, {"70", "3E", "B5", "66", "48", "03", "F6", "0E", "61", "35", "57", "B9", "86", "C1", "1D", "9E"}, {"E1", "F8", "98", "11", "69", "D9", "8E", "94", "9B", "1E", "87", "E9", "CE", "55", "28", "DF"}, {"8C", "A1", "89", "0D", "BF", "E6", "42", "68", "41", "99", "2D", "0F", "B0", "54", "BB", "16"}};
        String bs[][] = new String[4][4];   
        
        //byte substitution
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                int r, c;
                if (s1[i][j].length() < 2) {
                    r = 0;

                    if (s1[i][j].equals("a") || s1[i][j].equals("b") || s1[i][j].equals("c") || s1[i][j].equals("d") || s1[i][j].equals("e") || s1[i][j].equals("f")) {
                        c = s1[i][j].charAt(0) - 97 + 10;
                    } else {
                        c = s1[i][j].charAt(0) - 48;
                    }
                } else {

                    if (s1[i][j].charAt(0) == 'a' || s1[i][j].charAt(0) == 'b' || s1[i][j].charAt(0) == 'c' || s1[i][j].charAt(0) == 'd' || s1[i][j].charAt(0) == 'e' || s1[i][j].charAt(0) == 'f') {
                        r = s1[i][j].charAt(0) - 97 + 10;
                    } else {
                        r = s1[i][j].charAt(0) - 48;
                    }
                    if (s1[i][j].charAt(1) == 'a' || s1[i][j].charAt(1) == 'b' || s1[i][j].charAt(1) == 'c' || s1[i][j].charAt(1) == 'd' || s1[i][j].charAt(1) == 'e' || s1[i][j].charAt(1) == 'f') {
                        c = s1[i][j].charAt(1) - 97 + 10;
                    } else {
                        c = s1[i][j].charAt(1) - 48;
                    }
                }
                bs[i][j] = sbox[r][c];
            }
        }
        System.out.println();
        System.out.println("After byte substitution:");
        for (int i = 0; i < 4; i++) {
            System.out.println();
            for (int j = 0; j < 4; j++) {
                System.out.print(bs[i][j] + " ");
            }
        }
        //shift rows
        String t;
        t = bs[1][0];
        for (int i = 0; i < 3; i++) {
            bs[1][i] = bs[1][i + 1];
        }
        bs[1][3] = t;
        String temp;
        temp = bs[2][0];
        t = bs[2][1];
        bs[2][0] = bs[2][2];
        bs[2][1] = bs[2][3];
        bs[2][2] = temp;
        bs[2][3] = t;

        temp = bs[3][0];
        t = bs[3][1];
        String te;
        te = bs[3][2];
        bs[3][0] = bs[3][3];
        bs[3][1] = temp;
        bs[3][2] = t;
        bs[3][3] = te;
        System.out.println();
        System.out.println("After Shift rows");
        for (int i = 0; i < 4; i++) {
            System.out.println();
            for (int j = 0; j < 4; j++) {
                System.out.print(bs[i][j] + " ");
            }
        }
        //mixcolumns

        int mix[][] = {{2, 3, 1, 1}, {1, 2, 3, 1}, {1, 1, 2, 3}, {3, 1, 1, 2}};
        int mc[][] = new int[4][4];
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                mc[i][j] = Integer.parseInt(bs[i][j], 16);
            }
        }
        for (int i = 0; i < 4; i++) {
            System.out.println();
            for (int j = 0; j < 4; j++) {
                System.out.print(mc[i][j] + " ");
            }
        }
        int y = 283;
        int r[][] = new int[4][4];
        int x;
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                r[i][j] = 0;
                for (int ki = 0; ki < 4; ki++) {
                    System.out.println("value of i n j is " + i + j);
                    x = mc[ki][j];
                    switch (mix[i][ki]) {

                        case 2:
                            if (mc[ki][j] % 2 != 0) {
                                x = (x << 1) ^ y;
                            } else {
                                x = x << 1;
                            }
                            break;
                        case 3:
                            // System.out.println("value of mc is " + mc[ki][j] + " value of mix is " + mix[i][ki]);

                            // x = x << 1;
                            if (mc[ki][j] % 2 != 0) {
                                x = ((x << 1) ^ y) ^ x;
                                //   System.out.println("Before Xor with 11b x=" + x);
                                //x = x ^ y;
                                // System.out.println("After Xor with 11b x=" + x);
                            } else {
                                x = (x << 1) ^ x;
                            }
                            //x = x ^ mc[ki][j];
                            break;
                        default:
                            break;
                    }
                    r[i][j] = r[i][j] ^ x;
                }
            }
        }
        for (int i = 0; i < 4; i++) {
            System.out.println(); 
            for (int j = 0; j < 4; j++) {
                System.out.print(r[i][j] + " ");
            }
        }
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                bs[i][j] = Integer.toHexString(r[i][j]);
            }
        }
        System.out.println();
        System.out.println("After mix columns");
        for (int i = 0; i < 4; i++) {
            System.out.println();
            for (int j = 0; j < 4; j++) {
                System.out.print(bs[i][j] + " ");
            }
        }
    }
}

--------------DSS-----------
import java.util.*;
import java.math.BigInteger;

public class dss{
    public static BigInteger[] Sign(BigInteger msg, BigInteger e1, BigInteger d, BigInteger p, BigInteger q){
        Random random = new Random();
        BigInteger r = BigInteger.probablePrime(q.bitLength(), random);

        while(!r.gcd(q).equals(BigInteger.ONE)||r.compareTo(q)>0){
            r = BigInteger.probablePrime(q.bitLength(), random);
        }

        BigInteger s1 = e1.modPow(r,p).modPow(BigInteger.ONE, q);
        BigInteger s2 = ((msg.add(s1.multiply(d))).multiply(r.modInverse(q))).modPow(BigInteger.ONE, q);

        BigInteger[] ans = new BigInteger[2];
        ans[0] = s1;
        ans[1] = s2;

        System.out.println("r="+r);
        System.out.println("S1="+s1);
        System.out.println("S2="+s2);
        return ans;
    }

    public static boolean verify(BigInteger msg, BigInteger e1, BigInteger e2, BigInteger s1, BigInteger s2, BigInteger p, BigInteger q){
        BigInteger pow1 = msg.multiply(s2.modInverse(q));
        BigInteger pow2 = s1.multiply(s2.modInverse(q));

        BigInteger A = e1.modPow(pow1,p);
        BigInteger B = e2.modPow(pow2,p);
        BigInteger ans = A.multiply(B).mod(p).mod(q);
        System.out.println("V="+ans);
        return s1.equals(ans);

    }
        
    public static void main(String[] args){
        Random random = new Random();
        BigInteger p = BigInteger.probablePrime(1000, random);
        BigInteger q = BigInteger.probablePrime(20, random);

        while(!((p.subtract(BigInteger.ONE)).mod(q)).equals(BigInteger.ZERO)){
            p = BigInteger.probablePrime(26, random);
            q = BigInteger.probablePrime(12, random);
        }

        BigInteger e0 = p.subtract(BigInteger.ONE);
        do{
            if(e0.modPow(q,p).equals(BigInteger.ONE))
                break;
            e0 = e0.subtract(BigInteger.ONE);   
        }while(true);


        BigInteger d = q.subtract(BigInteger.ONE);
        do{
            d = BigInteger.probablePrime(d.bitLength(), random);            
        }while(d.compareTo(q)>0);

        BigInteger e1 = e0.modPow((p.subtract(BigInteger.ONE)).divide(q),p);
        BigInteger e2 = e1.modPow(d,p);

        System.out.println("p="+p);
        System.out.println("q="+q);
        System.out.println("e0="+e0);
        System.out.println("e1="+e1);
        System.out.println("e2="+e2);
        System.out.println("d="+d);

        BigInteger[] sign = Sign(BigInteger.valueOf(123),e1, d, p, q);
        System.out.println(verify(BigInteger.valueOf(123), e1, e2, sign[0], sign[1], p, q));
    }
}
-------------------DSS----------------
import java.io.*;
import java.util.*;
public class DSS
{
  public static int inverse (int b, int m)
  {
    int q, a1, a2, a3, b1, b2, b3, t1, t2, t3;
      a1 = 1;
      a2 = 0;
      a3 = m;
      b1 = 0;
      b2 = 1;
      b3 = b;
    while (b3 != 1)
      {
	q = a3 / b3;
	t1 = a1 - (q * b1);
	t2 = a2 - (q * b2);
	t3 = a3 - (q * b3);
	a1 = b1;
	a2 = b2;
	a3 = b3;
	b1 = t1;
	b2 = t2;
	b3 = t3;
      }
    return b2;
  }
  public static void main (String args[])
  {
    Scanner sc = new Scanner (System.in);
    System.out.println ("Enter the value of h(m),p,h,k,q,x");
    int hf = sc.nextInt ();
    int p = sc.nextInt ();
    int h = sc.nextInt ();
    int k = sc.nextInt ();
    int q = sc.nextInt ();
    int x = sc.nextInt ();
    int pow = (p - 1) / q;
    int g = 1;
    for (int i = 0; i < pow; i++)
      {
	g = (g * h) % p;
      }
    System.out.println (g);
    System.out.println ("global public keys:" + " " + p + "," + q + "," + g);
    int y = 1;
    for (int i = 0; i < x; i++)
      {
	y = (y * g) % p;
      }
    System.out.println ("public key" + " " + y);
    int r1 = 1;
    int r = 0;
    for (int i = 0; i < k; i++)
      {
	r1 = (r1 * g) % p;
	r = r1 % q;
      }
    System.out.println ("value of r" + " " + r);
    int invert = inverse (k, q);
    int t = x * r;
    int s1 = invert * (hf + t);
    int st = -s1;
    while (st > q)
      st = st % q;
    int s = q - st;
    System.out.println ("value of s" + " " + s);
    int w = inverse (s, q);
    System.out.println ("w" + w);
    int n1 = (hf * w) % q;
//System.out.println("n1"+n1);
    int n2 = (r * w);
    int st1 = -n2;
    if (st1 > q)
      {
	st1 = st1 % q;
      }
    int n21 = q - st1;
//System.out.println("n2"+n21);
    int v1 = 1;
    for (int i = 0; i < n1; i++)
      {
	v1 = v1 * g;
      }
    int v2 = 1;
    for (int i = 0; i < n21; i++)
      {
	v2 = v2 * y;
      }
    int v3 = (v1 * v2) % p;
    int v = v3 % q;
    System.out.println ("value of v" + " " + v);
    if (r == v)
      System.out.println ("Dss verified");
    else
      System.out.println ("Dss not verified");
  }
}
---------------------RSA--------------
import java.util.Scanner;

class Crypto{
    String alphabet = "abcdefghijklmnopqrstuvwxyz";

    public int modInverse(int a, int n){
        for(int i = 1; i < n; i++){
            if((a*i)% n == 1){
            return i;}
        }
        return -1;
    }

    public int modPower(int a, int e, int n){
        int result = 1;
        while(e > 0){
            if(e % 2 == 1){
                result = (result * a) % n;
            }
            a = (a*a) % n;
            e = e/2;
        }
        return result;
    }

    public String encrypt(String text, int e, int n){
        StringBuilder sb = new StringBuilder();
        for(char c : text.toCharArray()){
            int index = alphabet.indexOf(c);
            int encrypted  = modPower(index, e, n);
            sb.append(encrypted).append(" ");
        }
        return sb.toString();
    }
    public String decrypt(String text, int d, int n){
        StringBuilder sb = new StringBuilder();
        String[] parts = text.trim().split(" ");
        for(String part : parts){
            int index = Integer.parseInt(part);
            int decrypt = modPower(index, d, n);
            sb.append(alphabet.charAt(decrypt));
        }
        return sb.toString();
    }
}
class rsa{
    public static void main(String[] args){
        Scanner ss  = new Scanner(System.in);
        Crypto obj = new Crypto();
        System.out.print("Enter the text : ");
        String text = ss.nextLine();
        System.out.print("Enter prime number 1 : ");
        int p = ss.nextInt();
        System.out.print("Enter prime number 2 : ");
        int q = ss.nextInt();
        int n = p * q;
        int phi = (p-1) * (q-1);
        System.out.print("Enter the exponent value : ");
        int e = ss.nextInt();
        //check for gcd
        int d = obj.modInverse(e, phi);
        System.out.println("The private key : " + d);
        String encrypt = obj.encrypt(text, e, n);
        System.out.println("Encrypted text : " + encrypt);
        String decrypt = obj.decrypt(encrypt, d, n);
        System.out.println("Decrypted text : " + decrypt);
        ss.close();
    }
}
-----------------------SDES-----------------------

import java.io.*;
import java.lang.*;
class SDES
       {
        public int K1, K2;
        public static final int P10[] = { 3, 5, 2, 7, 4, 10, 1, 9, 8, 6};
        public static final int P10max = 10;
        public static final int P8[] = { 6, 3, 7, 4, 8, 5, 10, 9};
        public static final int P8max = 10;
        public static final int P4[] = { 2, 4, 3, 1};
        public static final int P4max = 4;
        public static final int IP[] = { 2, 6, 3, 1, 4, 8, 5, 7};
        public static final int IPmax = 8;
        public static final int IPI[] = { 4, 1, 3, 5, 7, 2, 8, 6};
        public static final int IPImax = 8;
        public static final int EP[] = { 4, 1, 2, 3, 2, 3, 4, 1};
        public static final int EPmax = 4;
        public static final int S0[][] = {{ 1, 0, 3, 2},{ 3, 2, 1, 0},{ 0, 2, 1,
                                                              3},{ 3, 1, 3, 2}};
        public static final int S1[][] = {{ 0, 1, 2, 3},{ 2, 0, 1, 3},{ 3, 0, 1,
                                                              2},{ 2, 1, 0, 3}};
       
       public static int permute( int x, int p[], int pmax)
       {
         int y = 0;
         for( int i = 0; i < p.length; ++i)
          {
            y <<= 1;
            y |= (x >> (pmax - p[i])) & 1;
        }
         return y;
       }

       public static int F( int R, int K)
       {
          int t = permute( R, EP, EPmax) ^ K;
          int t0 = (t >> 4) & 0xF;
          int t1 = t & 0xF;
          t0 = S0[ ((t0 & 0x8) >> 2) | (t0 & 1) ][ (t0 >> 1) & 0x3 ];
          t1 = S1[ ((t1 & 0x8) >> 2) | (t1 & 1) ][ (t1 >> 1) & 0x3 ];
           t = permute( (t0 << 2) | t1, P4, P4max);
         return t;
       
  }
          public static int fK( int m, int K)
                {
                    int L = (m >> 4) & 0xF;
                    int R = m & 0xF;
                    return ((L ^ F(R,K)) << 4) | R;
                }

          public static int SW( int x)
                      {
                      return ((x & 0xF) << 4) | ((x >> 4) & 0xF);
                      }

   public byte encrypt( int m)
       {
         System.out.println("\nEncryption Process Starts........\n\n"); 
          m = permute( m, IP, IPmax);

         System.out.print("\nAfter Permutation : ");
          printData( m, 8);

          m = fK( m, K1);
          System.out.print("\nbefore Swap : ");
          printData( m, 8);
          m = SW( m);
          System.out.print("\nAfter Swap : ");
          printData( m, 8);
          m = fK( m, K2);
          System.out.print("\nbefore IP inverse : ");
          printData( m, 8);
          m = permute( m, IPI, IPImax);
          return (byte) m;
       
        }
        public byte decrypt( int m)
       
        {
          System.out.println("\nDecryption Process Starts........\n\n");
          printData( m, 8);
          m = permute( m, IP, IPmax);
          System.out.print("\nAfter Permutation : ");
          printData( m, 8);
          m = fK( m, K2);
          System.out.print("\nbefore Swap : ");
          printData( m, 8);
          m = SW( m);
          System.out.print("\nAfter Swap : ");
          printData( m, 8);
          m = fK( m, K1);
          System.out.print("\nBefore Extraction Permutation : ");
          printData( m, 4);
          m = permute( m, IPI, IPImax);
          System.out.print("\nAfter Extraction Permutation : ");
          printData( m, 8);
          return (byte) m;
        }

        public static void printData( int x, int n)
         {
           int mask = 1 << (n-1);
           while( mask > 0)
           {
           System.out.print( ((x & mask) == 0) ? '0' : '1');
           mask >>= 1;
           }
        }

       public SDES( int K)
      {
          K = permute( K, P10, P10max);
          int t1 = (K >> 5) & 0x1F;
          int t2 = K & 0x1F;
          t1 = ((t1 & 0xF) << 1) | ((t1 & 0x10) >> 4);
          t2 = ((t2 & 0xF) << 1) | ((t2 & 0x10) >> 4);
          K1 = permute( (t1 << 5)| t2, P8, P8max);
          t1 = ((t1 & 0x7) << 2) | ((t1 & 0x18) >> 3);
          t2 = ((t2 & 0x7) << 2) | ((t2 & 0x18) >> 3);
          K2 = permute( (t1 << 5)| t2, P8, P8max);
       
        }
       
      }


public class SimplifiedDES
      {
       
        public static void main( String args[]) throws Exception
        {
         DataInputStream inp=new DataInputStream(System.in);
         System.out.println("Enter the 10 Bit Key :");
          int K = Integer.parseInt(inp.readLine(),2);
          SDES A = new SDES( K);

          System.out.println("Enter the 8 Bit message To be Encrypt  : ");
          int m = Integer.parseInt(inp.readLine(),2);

          System.out.print("\nKey K1: ");
          SDES.printData( A.K1, 8);
          System.out.print("\nKey K2: ");
          SDES.printData( A.K2, 8);

          m = A.encrypt( m);
          System.out.print("\nEncrypted Message: ");
          SDES.printData( m, 8);

          m = A.decrypt( m);
          System.out.print("\nDecrypted Message: ");
          SDES.printData( m, 8);
       
        }
       
    }
------------------------------SHA-------------------------
import struct
import binascii

init_hash = (
    0x6a09e667f3bcc908, 0xbb67ae8584caa73b, 0x3c6ef372fe94f82b, 0xa54ff53a5f1d36f1,
    0x510e527fade682d1, 0x9b05688c2b3e6c1f, 0x1f83d9abfb41bd6b, 0x5be0cd19137e2179,
)

rnd_consts = (0x428a2f98d728ae22,)

def _right_rotate(n, bits):
    return (n >> bits) | (n << (64 - bits)) & 0xFFFFFFFFFFFFFFFF

def sha512_one_round(message):
    msg_bytes = bytearray(message, 'utf-8')
    padding = [0x80] + [0] * (119 - len(msg_bytes) % 128) + list(struct.pack('!Q', len(msg_bytes) << 3))
    msg_bytes += bytearray(padding[-(128 - len(msg_bytes) % 128):])

    hash_vals = list(init_hash)
    for i in range(0, len(msg_bytes), 128):
        w = list(struct.unpack('!16Q', msg_bytes[i:i + 128]))
        a, b, c, d, e, f, g, h = hash_vals
        s1 = _right_rotate(e, 14) ^ _right_rotate(e, 18) ^ _right_rotate(e, 41)
        ch = (e & f) ^ (~e & g)
        t1 = h + s1 + ch + rnd_consts[0] + w[0]
        s0 = _right_rotate(a, 28) ^ _right_rotate(a, 34) ^ _right_rotate(a, 39)
        maj = (a & b) ^ (a & c) ^ (b & c)
        t2 = s0 + maj
        h, g, f, e, d, c, b, a = g, f, e, (d + t1) & 0xFFFFFFFFFFFFFFFF, c, b, a, (t1 + t2) & 0xFFFFFFFFFFFFFFFF
        hash_vals = [(x + y) & 0xFFFFFFFFFFFFFFFF for x, y in zip(hash_vals, (a, b, c, d, e, f, g, h))]

    return binascii.hexlify(b''.join(struct.pack('!Q', h) for h in hash_vals)).decode('utf-8')

print("Enter the message")
print("The result after one round is:", sha512_one_round(input()))

---------------------SHAJAVA----------------

import java.util.Scanner;
import java.security.NoSuchAlgorithmException;
import java.security.MessageDigest;
import java.nio.charset.StandardCharsets;
import java.math.BigInteger;

class SHA{
    public static byte[] getSHA(String text) throws NoSuchAlgorithmException{
        MessageDigest md = MessageDigest.getInstance("SHA-512");
        return md.digest(text.getBytes(StandardCharsets.UTF_8));
    }
    
    public static String toHex(byte[] hash){
        BigInteger num = new BigInteger(1, hash);
        StringBuilder sb = new StringBuilder(num.toString(16));
        while(sb.length() < 32){
            sb.append("0");
        }
        return sb.toString();
    }
    public static void main(String[] args){
        try{
            Scanner ss = new Scanner(System.in);
            System.out.println("Enter the text :");
            String text = ss.nextLine();
            System.out.println("Hash : " + toHex(getSHA(text)));
        }catch(NoSuchAlgorithmException e){
            System.out.println(e);
        }
    }
}


------------------------HILL---------------
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
public class hi
{
    int keymatrix[][];
    int linematrix[];
    int resultmatrix[];
    public void divide(String temp, int s)
    {
        while (temp.length() > s)
        {
            String sub = temp.substring(0, s);
            temp = temp.substring(s, temp.length());
            perform(sub);
        }
        if (temp.length() == s)
            perform(temp);
        else if (temp.length() < s)
        {
            for (int i = temp.length(); i < s; i++)
                temp = temp + 'x';
            perform(temp);
        }
    }
    public void perform(String line)
    {
        linetomatrix(line);
        linemultiplykey(line.length());
        result(line.length());
    }
    public void keytomatrix(String key, int len)
    {
        keymatrix = new int[len][len];
        int c = 0;
        for (int i = 0; i < len; i++)
        {
            for (int j = 0; j < len; j++)
            {
                keymatrix[i][j] = ((int) key.charAt(c)) - 97;
                c++;
            }
        }
    }
    public void linetomatrix(String line)
    {
        linematrix = new int[line.length()];
        for (int i = 0; i < line.length(); i++)
        {
            linematrix[i] = ((int) line.charAt(i)) - 97;
        }
    }
     public void linemultiplykey(int len)
    {
        resultmatrix = new int[len];
        for (int i = 0; i < len; i++)
        {
            for (int j = 0; j < len; j++)
            {
                resultmatrix[i] += keymatrix[i][j] * linematrix[j];
            }
            resultmatrix[i] %= 26;
        }
    }
    public void result(int len)
    {
        String result = "";
        for (int i = 0; i < len; i++)
        {
            result += (char) (resultmatrix[i] + 97);
        }
        System.out.print(result);
    }
    public boolean check(String key, int len)
    {
        keytomatrix(key, len);
        int d = determinant(keymatrix, len);
        d = d % 26;
        if (d == 0)
        {
            System.out.println("Invalid key!!! Key is not invertible because determinant=0...");
            return false;
        }
        else if (d % 2 == 0 || d % 13 == 0)
        {
            System.out.println("Invalid key!!! Key is not invertible because determinant has common factor with 26...");
            return false;
        }
        else
        {
            return true;
        }
    }
     public int determinant(int A[][], int N)
    {
        int res;
        if (N == 1)
            res = A[0][0];
        else if (N == 2)
        {
            res = A[0][0] * A[1][1] - A[1][0] * A[0][1];
        }
        else
        {
            res = 0;
            for (int j1 = 0; j1 < N; j1++)
            {
                int m[][] = new int[N - 1][N - 1];
                for (int i = 1; i < N; i++)
                {
                    int j2 = 0;
                    for (int j = 0; j < N; j++)
                    {
                        if (j == j1)
                            continue;
                        m[i - 1][j2] = A[i][j];
                        j2++;
                    }
                }
                res += Math.pow(-1.0, 1.0 + j1 + 1.0) * A[0][j1] * determinant(m, N - 1);
            }
        }
        return res;
    }
     public void cofact(int num[][], int f)
    {
        int b[][], fac[][];
        b = new int[f][f];
        fac = new int[f][f];
        int p, q, m, n, i, j;
        for (q = 0; q < f; q++)
        {
            for (p = 0; p < f; p++)
            {
                m = 0;
                n = 0;
                for (i = 0; i < f; i++)
                {
                    for (j = 0; j < f; j++)
                    {
                        b[i][j] = 0;
                        if (i != q && j != p)
                        {
                            b[m][n] = num[i][j];
                            if (n < (f - 2))
                                n++;
                            else
                            {
                                n = 0;
                                m++;
                            }
                        }
                    }
                }
                fac[q][p] = (int) Math.pow(-1, q + p) * determinant(b, f - 1);
            }
        }
        trans(fac, f);
    }
    void trans(int fac[][], int r)
    {
        int i, j;
        int b[][], inv[][];
        b = new int[r][r];
        inv = new int[r][r];
        int d = determinant(keymatrix, r);
        int mi = mi(d % 26);
        mi %= 26;
        if (mi < 0)
            mi += 26;
        for (i = 0; i < r; i++)
        {
            for (j = 0; j < r; j++)
            {
                b[i][j] = fac[j][i];
            }
        }
        for (i = 0; i < r; i++)
        {
            for (j = 0; j < r; j++)
            {
                inv[i][j] = b[i][j] % 26;
                if (inv[i][j] < 0)
                    inv[i][j] += 26;
                inv[i][j] *= mi;
                inv[i][j] %= 26;
            }
        }
        System.out.println("\nInverse key:");
        matrixtoinvkey(inv, r);
    }
    public int mi(int d)
    {
        int q, r1, r2, r, t1, t2, t;
        r1 = 26;
        r2 = d;
        t1 = 0;
        t2 = 1;
        while (r1 != 1 && r2 != 0)
        {
            q = r1 / r2;
            r = r1 % r2;
            t = t1 - (t2 * q);
            r1 = r2;
            r2 = r;
            t1 = t2;
            t2 = t;
        }
        return (t1 + t2);
    }
     public void matrixtoinvkey(int inv[][], int n)
    {
        String invkey = "";
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                invkey += (char) (inv[i][j] + 97);
            }
        }
        System.out.print(invkey);
    }
     public static void main(String args[]) throws IOException
    {
        hi obj = new hi();
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        int choice;
        System.out.println("Choose from the below options :\n1: Encryption\n2: Decryption");
        choice = Integer.parseInt(in.readLine());
        System.out.println("Enter the line: ");
        String line = in.readLine();
        System.out.println("Enter the key: ");
        String key = in.readLine();
        double sq = Math.sqrt(key.length());
        if (sq != (long) sq)
            System.out.println("Invalid key length!!! Does not form a square matrix...");
        else
        {
            int s = (int) sq;
            if (obj.check(key, s))
            {
                System.out.println("Result:");
                obj.divide(line, s);
                obj.cofact(obj.keymatrix, s);
            }
        }
    }
}

---------------HILL ATTACK-----------
import java.io.IOException;
import java.util.Scanner;

public class hillcryp {
    int keymatrix[][];
    int linematrix[];
    int resultmatrix[];
    String toSend;

    public void divide(String temp, int s) {
        toSend = "";
        while (temp.length() > s) {
            String sub = temp.substring(0, s);
            temp = temp.substring(s, temp.length());
            perform(sub);
        }
        if (temp.length() == s)
            perform(temp);
        else if (temp.length() < s) {
            for (int i = temp.length(); i < s; i++)
                temp = temp + 'x';
            perform(temp);
        }
    }

    public void perform(String line) {
        linetomatrix(line);
        linemultiplykey(line.length());
        result(line.length());
    }

    public void keytomatrix(String key, int len) {
        keymatrix = new int[len][len];
        int c = 0;
        for (int i = 0; i < len; i++) {
            for (int j = 0; j < len; j++) {
                keymatrix[i][j] = ((int) key.charAt(c)) - 97;
                c++;
            }
        }
    }

    public void linetomatrix(String line) {
        linematrix = new int[line.length()];
        for (int i = 0; i < line.length(); i++) {
            linematrix[i] = ((int) line.charAt(i)) - 97;
        }
    }

    public void linemultiplykey(int len) {
        resultmatrix = new int[len];
        for (int i = 0; i < len; i++) {
            for (int j = 0; j < len; j++) {
                resultmatrix[i] += keymatrix[i][j] * linematrix[j];
            }
            resultmatrix[i] %= 26;
        }
    }

    public void result(int len) {
        String result = "";
        for (int i = 0; i < len; i++) {
            result += (char) (resultmatrix[i] + 97);
        }
        toSend = toSend + result;
        System.out.print(result);
    }

    public boolean check(String key, int len) {
        keytomatrix(key, len);
        int d = determinant(keymatrix, len);
        d = d % 26;
        if (d == 0) {
            // System.out
            // .println("Invalid key!!! Key is not invertible because determinant=0...");
            return false;
        } else if (d % 2 == 0 || d % 13 == 0) {
            // System.out
            // .println("Invalid key!!! Key is not invertible because determinant has common
            // factor with 26...");
            return false;
        } else {
            return true;
        }
    }

    public int determinant(int A[][], int N) {
        int res;
        if (N == 1)
            res = A[0][0];
        else if (N == 2) {
            res = A[0][0] * A[1][1] - A[1][0] * A[0][1];
        } else {
            res = 0;
            for (int j1 = 0; j1 < N; j1++) {
                int m[][] = new int[N - 1][N - 1];
                for (int i = 1; i < N; i++) {
                    int j2 = 0;
                    for (int j = 0; j < N; j++) {
                        if (j == j1)
                            continue;
                        m[i - 1][j2] = A[i][j];
                        j2++;
                    }
                }
                res += Math.pow(-1.0, 1.0 + j1 + 1.0) * A[0][j1]
                        * determinant(m, N - 1);
            }
        }
        return res;
    }

    public void cofact(int num[][], int f) {
        int b[][], fac[][];
        b = new int[f][f];
        fac = new int[f][f];
        int p, q, m, n, i, j;
        for (q = 0; q < f; q++) {
            for (p = 0; p < f; p++) {
                m = 0;
                n = 0;
                for (i = 0; i < f; i++) {
                    for (j = 0; j < f; j++) {
                        b[i][j] = 0;
                        if (i != q && j != p) {
                            b[m][n] = num[i][j];
                            if (n < (f - 2))
                                n++;
                            else {
                                n = 0;
                                m++;
                            }
                        }
                    }
                }
                fac[q][p] = (int) Math.pow(-1, q + p) * determinant(b, f - 1);
            }
        }
        trans(fac, f);
    }

    void trans(int fac[][], int r) {
        int i, j;
        int b[][], inv[][];
        b = new int[r][r];
        inv = new int[r][r];
        int d = determinant(keymatrix, r);
        int mi = mi(d % 26);
        mi %= 26;
        if (mi < 0)
            mi += 26;
        for (i = 0; i < r; i++) {
            for (j = 0; j < r; j++) {
                b[i][j] = fac[j][i];
            }
        }
        for (i = 0; i < r; i++) {
            for (j = 0; j < r; j++) {
                inv[i][j] = b[i][j] % 26;
                if (inv[i][j] < 0)
                    inv[i][j] += 26;
                inv[i][j] *= mi;
                inv[i][j] %= 26;
            }
        }
        // System.out.println("\nInverse key:");
        matrixtoinvkey(inv, r);
    }

    public int mi(int d) {
        int q, r1, r2, r, t1, t2, t;
        r1 = 26;
        r2 = d;
        t1 = 0;
        t2 = 1;
        while (r1 != 1 && r2 != 0) {
            q = r1 / r2;
            r = r1 % r2;
            t = t1 - (t2 * q);
            r1 = r2;
            r2 = r;
            t1 = t2;
            t2 = t;
        }
        return (t1 + t2);
    }

    public void matrixtoinvkey(int inv[][], int n) {
        String invkey = "";
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                invkey += (char) (inv[i][j] + 97);
            }
        }
        // System.out.print(invkey);
    }

    public static void main(String args[]) throws IOException {
        Scanner sc = new Scanner(System.in);
        hillcryp obj = new hillcryp();
        System.out.println("Enter the plain text:");
        String plainText = sc.nextLine();
        System.out.println("Enter Encrypted text:");
        String encryptedText = sc.next();

        int stringLength = 4;
        char[] charset = "abcdefghijklmnopqrstuvwxyz".toCharArray();

        int totalCombinations = (int) Math.pow(charset.length, stringLength);

        for (int i = 0; i < totalCombinations; i++) {
            StringBuilder sb = new StringBuilder();
            int index = i;

            for (int j = 0; j < stringLength; j++) {
                sb.append(charset[index % charset.length]);
                index /= charset.length;
            }

            String key = sb.toString();
            double sq = Math.sqrt(key.length());

            System.out.println(sb.toString());

            int s = (int) sq;
            if (obj.check(key, s)) {
                System.out.println("Result:");
                obj.divide(plainText, s);
                obj.cofact(obj.keymatrix, s);
                if (obj.toSend.equals(encryptedText)) {
                    System.out.println("\n\nKey: " + key);
                    System.out.println("Plaintext: " + plainText);
                    System.out.println("Encrypted text: " + encryptedText);
                    break;
                }
            }
        }
    }
}

------------------RAILFENCE-----------------
// C++ program to illustrate Rail Fence Cipher
// Encryption and Decryption
import java.util.Arrays;
class RailFence {

	// function to encrypt a message
	public static String encryptRailFence(String text,
										int key)
	{

		// create the matrix to cipher plain text
		// key = rows , length(text) = columns
		char[][] rail = new char[key][text.length()];

		// filling the rail matrix to distinguish filled
		// spaces from blank ones
		for (int i = 0; i < key; i++)
			Arrays.fill(rail[i], '\n');

		boolean dirDown = false;
		int row = 0, col = 0;

		for (int i = 0; i < text.length(); i++) {

			// check the direction of flow
			// reverse the direction if we've just
			// filled the top or bottom rail
			if (row == 0 || row == key - 1)
				dirDown = !dirDown;

			// fill the corresponding alphabet
			rail[row][col++] = text.charAt(i);

			// find the next row using direction flag
			if (dirDown)
				row++;
			else
				row--;
		}

		// now we can construct the cipher using the rail
		// matrix
		StringBuilder result = new StringBuilder();
		for (int i = 0; i < key; i++)
			for (int j = 0; j < text.length(); j++)
				if (rail[i][j] != '\n')
					result.append(rail[i][j]);

		return result.toString();
	}

	// This function receives cipher-text and key
	// and returns the original text after decryption
	public static String decryptRailFence(String cipher,
										int key)
	{

		// create the matrix to cipher plain text
		// key = rows , length(text) = columns
		char[][] rail = new char[key][cipher.length()];

		// filling the rail matrix to distinguish filled
		// spaces from blank ones
		for (int i = 0; i < key; i++)
			Arrays.fill(rail[i], '\n');

		// to find the direction
		boolean dirDown = true;

		int row = 0, col = 0;

		// mark the places with '*'
		for (int i = 0; i < cipher.length(); i++) {
			// check the direction of flow
			if (row == 0)
				dirDown = true;
			if (row == key - 1)
				dirDown = false;

			// place the marker
			rail[row][col++] = '*';

			// find the next row using direction flag
			if (dirDown)
				row++;
			else
				row--;
		}

		// now we can construct the fill the rail matrix
		int index = 0;
		for (int i = 0; i < key; i++)
			for (int j = 0; j < cipher.length(); j++)
				if (rail[i][j] == '*'
					&& index < cipher.length())
					rail[i][j] = cipher.charAt(index++);

		StringBuilder result = new StringBuilder();

		row = 0;
		col = 0;
		for (int i = 0; i < cipher.length(); i++) {
			// check the direction of flow
			if (row == 0)
				dirDown = true;
			if (row == key - 1)
				dirDown = false;

			// place the marker
			if (rail[row][col] != '*')
				result.append(rail[row][col++]);

			// find the next row using direction flag
			if (dirDown)
				row++;
			else
				row--;
		}
		return result.toString();
	}

	// driver program to check the above functions
	public static void main(String[] args)
	{

		// Encryption
		System.out.println("Encrypted Message: ");
		System.out.println(
			encryptRailFence("attack at once", 2));
		System.out.println(
			encryptRailFence("GeeksforGeeks ", 3));
		System.out.println(
			encryptRailFence("defend the east wall", 3));

		// Now decryption of the same cipher-text
		System.out.println("\nDecrypted Message: ");
		System.out.println(
			decryptRailFence("atc toctaka ne", 2));
		System.out.println(
			decryptRailFence("GsGsekfrek eoe", 3));
		System.out.println(
			decryptRailFence("dnhaweedtees alf tl", 3));
	}
}
--------------------COLUMNAR---------------
import java.util.Arrays;

public class ColumnarMatrixCipher {
    public static String encrypt(String plaintext, String key) {
        int keyLength = key.length();
        int textLength = plaintext.length();
        int rows = (int) Math.ceil((double) textLength / keyLength);
        char[][] matrix = new char[rows][keyLength];

        // Fill the matrix with the plaintext characters
        int charIndex = 0;
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < keyLength; col++) {
                if (charIndex < textLength) {
                    matrix[row][col] = plaintext.charAt(charIndex);
                    charIndex++;
                } else {
                    matrix[row][col] = ' ';
                }
            }
        }

        // Sort the columns based on the key
        char[] keyChars = key.toCharArray();
        Arrays.sort(keyChars);

        // Create the ciphertext by reading the matrix column by column
        StringBuilder ciphertext = new StringBuilder();
        for (char keyChar : keyChars) {
            int col = key.indexOf(keyChar);
            for (int row = 0; row < rows; row++) {
                ciphertext.append(matrix[row][col]);
            }
        }

        return ciphertext.toString();
    }

    public static String decrypt(String ciphertext, String key) {
        int keyLength = key.length();
        int textLength = ciphertext.length();
        int rows = (int) Math.ceil((double) textLength / keyLength);
        char[][] matrix = new char[rows][keyLength];

        // Calculate the number of characters in the last column
        int charsInLastCol = textLength % keyLength;
        
        // Calculate the number of full columns
        int fullCols = keyLength - charsInLastCol;

        // Calculate the split point for the key
        int splitPoint = keyLength - fullCols;

        // Sort the columns based on the key up to the split point
        char[] keyChars = key.substring(0, splitPoint).toCharArray();
        Arrays.sort(keyChars);

        int ciphertextIndex = 0;
        for (int col = 0; col < splitPoint; col++) {
            char keyChar = keyChars[col];
            int colIndex = key.indexOf(keyChar);
            for (int row = 0; row < rows; row++) {
                matrix[row][colIndex] = ciphertext.charAt(ciphertextIndex);
                ciphertextIndex++;
            }
        }

        // Sort the columns based on the remaining key characters
        keyChars = key.substring(splitPoint).toCharArray();
        Arrays.sort(keyChars);

        for (int col = splitPoint; col < keyLength; col++) {
            char keyChar = keyChars[col - splitPoint];
            int colIndex = key.indexOf(keyChar);
            for (int row = 0; row < rows; row++) {
                matrix[row][colIndex] = ciphertext.charAt(ciphertextIndex);
                ciphertextIndex++;
            }
        }

        // Read the matrix row by row to obtain the plaintext
        StringBuilder plaintext = new StringBuilder();
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < keyLength; col++) {
                plaintext.append(matrix[row][col]);
            }
        }

        return plaintext.toString().trim();
    }

    public static void main(String[] args) {
        String plaintext = "HELLO WORLD";
        String key = "COLUMNAR";
        String ciphertext = encrypt(plaintext, key);
        System.out.println("Encrypted: " + ciphertext);
        String decrypted = decrypt(ciphertext, key);
        System.out.println("Decrypted: " + decrypted);
    }
----------------------VIGENERE-----------------
public class VigenereCipher {
    public static String encrypt(String plaintext, String key) {
        StringBuilder ciphertext = new StringBuilder();
        plaintext = plaintext.toUpperCase(); // Convert plaintext to uppercase for consistency

        for (int i = 0, j = 0; i < plaintext.length(); i++) {
            char c = plaintext.charAt(i);
            if (Character.isLetter(c)) {
                int shift = key.charAt(j % key.length()) - 'A';
                char encryptedChar = (char) (((c - 'A' + shift) % 26) + 'A');
                ciphertext.append(encryptedChar);
                j++;
            } else {
                ciphertext.append(c); // Non-alphabetic characters are not modified
            }
        }

        return ciphertext.toString();
    }

    public static String decrypt(String ciphertext, String key) {
        StringBuilder plaintext = new StringBuilder();
        ciphertext = ciphertext.toUpperCase(); // Convert ciphertext to uppercase for consistency

        for (int i = 0, j = 0; i < ciphertext.length(); i++) {
            char c = ciphertext.charAt(i);
            if (Character.isLetter(c)) {
                int shift = key.charAt(j % key.length()) - 'A';
                char decryptedChar = (char) (((c - 'A' - shift + 26) % 26) + 'A');
                plaintext.append(decryptedChar);
                j++;
            } else {
                plaintext.append(c); // Non-alphabetic characters are not modified
            }
        }

        return plaintext.toString();
    }

    public static void main(String[] args) {
        String plaintext = "HELLO WORLD";
        String key = "KEY";

        String ciphertext = encrypt(plaintext, key);
        String decrypted = decrypt(ciphertext, key);

        System.out.println("Plaintext: " + plaintext);
        System.out.println("Ciphertext: " + ciphertext);
        System.out.println("Decrypted: " + decrypted);
    }
}
--------------------------------VERNAM-----------
public class VernamCipher {
    public static String encrypt(String plaintext, String key) {
        if (plaintext.length() != key.length()) {
            throw new IllegalArgumentException("Key length must match plaintext length");
        }

        StringBuilder ciphertext = new StringBuilder();
        for (int i = 0; i < plaintext.length(); i++) {
            char plainChar = plaintext.charAt(i);
            char keyChar = key.charAt(i);

            // XOR the characters
            char encryptedChar = (char) (plainChar ^ keyChar);
            ciphertext.append(encryptedChar);
        }

        return ciphertext.toString();
    }

    public static String decrypt(String ciphertext, String key) {
        return encrypt(ciphertext, key); // XOR operation is reversible
    }

    public static void main(String[] args) {
        String plaintext = "HELLO";
        String key = "SECRET";

        String ciphertext = encrypt(plaintext, key);
        String decrypted = decrypt(ciphertext, key);

        System.out.println("Plaintext: " + plaintext);
        System.out.println("Key: " + key);
        System.out.println("Ciphertext: " + ciphertext);
        System.out.println("Decrypted: " + decrypted);
    }
}

---------------------------DEFFIE HELMAN--------------
// This program calculates the Key for two persons
// using the Diffie-Hellman Key exchange algorithm
class GFG {

	// Power function to return value of a ^ b mod P
	private static long power(long a, long b, long p)
	{
		if (b == 1)
			return a;
		else
			return (((long)Math.pow(a, b)) % p);
	}

	// Driver code
	public static void main(String[] args)
	{
		long P, G, x, a, y, b, ka, kb;

		// Both the persons will be agreed upon the
		// public keys G and P

		// A prime number P is taken
		P = 23;
		System.out.println("The value of P:" + P);

		// A primitive root for P, G is taken
		G = 9;
		System.out.println("The value of G:" + G);

		// Alice will choose the private key a
		// a is the chosen private key
		a = 4;
		System.out.println("The private key a for Alice:"
						+ a);

		// Gets the generated key
		x = power(G, a, P);

		// Bob will choose the private key b
		// b is the chosen private key
		b = 3;
		System.out.println("The private key b for Bob:"
						+ b);

		// Gets the generated key
		y = power(G, b, P);

		// Generating the secret key after the exchange
		// of keys
		ka = power(y, a, P); // Secret key for Alice
		kb = power(x, b, P); // Secret key for Bob

		System.out.println("Secret key for the Alice is:"
						+ ka);
		System.out.println("Secret key for the Bob is:"
						+ kb);
	}
}


-----------------------------------------------
-----------------------------------------------
-----------------------------------------------

CAlculator

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:background="@color/black"
    android:padding="20dp">

    <TextView
        android:id="@+id/screen"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:text="0"
        android:textStyle="bold"
        android:textSize="60dp"
        android:textColor="#FFFFFF"
        android:paddingHorizontal="15dp"
        android:paddingVertical="35dp"
        android:layout_above="@+id/nums"/>

    <LinearLayout
        android:id="@+id/nums"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:orientation="horizontal"
        android:paddingTop="20dp">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="vertical">

            <Button
                android:id="@+id/on"
                android:text="ON"
                style="@style/Button1" />

            <Button
                android:id="@+id/num7"
                android:text="7"
                style="@style/Button2" />

            <Button
                android:id="@+id/num4"
                android:text="4"
                style="@style/Button2"/>

            <Button
                android:id="@+id/num1"
                android:text="1"
                style="@style/Button2"/>

            <Button
                android:id="@+id/del"
                android:text="del"
                style="@style/Button1"/>

        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="vertical">

            <Button
                android:id="@+id/off"
                android:text="off"
                style="@style/Button1"/>

            <Button
                android:id="@+id/num8"
                android:text="8"
                style="@style/Button2"/>

            <Button
                android:id="@+id/num5"
                android:text="5"
                style="@style/Button2"/>

            <Button
                android:id="@+id/num2"
                android:text="2"
                style="@style/Button2"/>

            <Button
                android:id="@+id/num0"
                android:text="0"
                style="@style/Button2"/>

        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="vertical">

            <Button
                android:id="@+id/ac"
                android:text="ac"
                style="@style/Button1"/>

            <Button
                android:id="@+id/num9"
                android:text="9"
                style="@style/Button2"/>

            <Button
                android:id="@+id/num6"
                android:text="6"
                style="@style/Button2"/>

            <Button
                android:id="@+id/num3"
                android:text="3"
                style="@style/Button2"/>

            <Button
                android:id="@+id/point"
                android:text="."
                style="@style/Button2"/>

        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="vertical">

            <Button
                android:id="@+id/div"
                android:text="/"
                style="@style/Button1"/>

            <Button
                android:id="@+id/times"
                android:text="*"
                style="@style/Button1"/>

            <Button
                android:id="@+id/min"
                android:text="-"
                style="@style/Button1"/>

            <Button
                android:id="@+id/plus"
                android:text="+"
                style="@style/Button1"/>

            <Button
                android:id="@+id/equal"
                android:text="="
                style="@style/Button1"/>

        </LinearLayout>
    </LinearLayout>
</RelativeLayout>


package com.example.calculator;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.app.NotificationCompat;
import androidx.core.app.NotificationManagerCompat;

import android.app.NotificationChannel;
import android.app.NotificationManager;
import android.content.pm.PackageManager;
import android.os.Build;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.ArrayList;
import java.util.regex.Pattern;

public class MainActivity extends AppCompatActivity {

    double firstNum;
    String operation;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button num0 = findViewById(R.id.num0);
        Button num1 = findViewById(R.id.num1);
        Button num2 = findViewById(R.id.num2);
        Button num3 = findViewById(R.id.num3);
        Button num4 = findViewById(R.id.num4);
        Button num5 = findViewById(R.id.num5);
        Button num6 = findViewById(R.id.num6);
        Button num7 = findViewById(R.id.num7);
        Button num8 = findViewById(R.id.num8);
        Button num9 = findViewById(R.id.num9);

        Button on = findViewById(R.id.on);
        Button off = findViewById(R.id.off);
        Button ac = findViewById(R.id.ac);
        Button del = findViewById(R.id.del);
        Button div = findViewById(R.id.div);
        Button times = findViewById(R.id.times);
        Button min = findViewById(R.id.min);
        Button equal = findViewById(R.id.equal);
        Button plus = findViewById(R.id.plus);
        Button point = findViewById(R.id.point);

        TextView screen = findViewById(R.id.screen);

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            NotificationChannel ch = new NotificationChannel("calculator_channel", "Calculator Channel",
                    NotificationManager.IMPORTANCE_DEFAULT);
            NotificationManager manager = getSystemService(NotificationManager.class);
            manager.createNotificationChannel(ch);
        }


        ac.setOnClickListener(view -> {
            firstNum = 0;
            screen.setText("0");
        });

        off.setOnClickListener(view -> screen.setVisibility(View.GONE));
        on.setOnClickListener(view -> {
            screen.setVisibility(View.VISIBLE);
            screen.setText("0");
        });

        ArrayList<Button> nums = new ArrayList<>();
        nums.add(num0);
        nums.add(num1);
        nums.add(num2);
        nums.add(num3);
        nums.add(num4);
        nums.add(num5);
        nums.add(num6);
        nums.add(num7);
        nums.add(num8);
        nums.add(num9);

        for (Button b : nums) {
            b.setOnClickListener(view -> {
                if (!screen.getText().toString().equals("0")) {
                    screen.setText(screen.getText().toString() + b.getText().toString());
                } else {
                    screen.setText(b.getText().toString());
                }
            });
        }

        ArrayList<Button> opers = new ArrayList<>();
        opers.add(div);
        opers.add(times);
        opers.add(plus);
        opers.add(min);

        for (Button b : opers) {
            b.setOnClickListener(view -> {
                firstNum = Double.parseDouble(screen.getText().toString());
                operation = b.getText().toString();
                screen.setText("");
            });
        }




        del.setOnClickListener(view -> {
            String num = screen.getText().toString();
            if (num.length() > 1) {
                screen.setText(num.substring(0, num.length() - 1));
            } else if (num.length() == 1 && !num.equals("0")) {
                screen.setText("0");
            }
        });

        point.setOnClickListener(view -> {
            if (!screen.getText().toString().contains(".")) {
                screen.setText(screen.getText().toString() + ".");
            }
        });

        equal.setOnClickListener(view -> {
            if (!screen.getText().toString().isEmpty()) {
                double secondNum = Double.parseDouble(screen.getText().toString());
                double result;
                switch (operation) {
                    case "/":
                        result = firstNum / secondNum;
                        break;
                    case "*":
                        result = firstNum * secondNum;
                        break;
                    case "+":
                        result = firstNum + secondNum;
                        break;
                    case "-":
                        result = firstNum - secondNum;
                        break;
                    default:
                        result = 0;
                }
                screen.setText(String.valueOf(result));
                showNotification("Calculator Result", String.valueOf(result));
            }
        });

    }

    private void showNotification(String calculatorResult, String valueOf) {
        NotificationCompat.Builder builder = new NotificationCompat.Builder(this, "calculator_channel")
                .setSmallIcon(R.drawable.ic_launcher_foreground)
                .setContentTitle(calculatorResult)
                .setContentText(valueOf)
                .setPriority(NotificationCompat.PRIORITY_DEFAULT);

        NotificationManagerCompat notificationManager = NotificationManagerCompat.from(this);
        if (ActivityCompat.checkSelfPermission(this, android.Manifest.permission.POST_NOTIFICATIONS) != PackageManager.PERMISSION_GRANTED) {
            return;
        }
        notificationManager.notify(1, builder.build());
    }
}

<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <solid android:color="#00BCD4"/>
</shape>


<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <solid android:color="#3F51B5"/>
</shape>


<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Theme.Calculator" parent="Theme.AppCompat.Light.NoActionBar">
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/black</item>
        <item name="colorPrimaryVariant">@color/black</item>
        <item name="colorOnPrimary">@color/white</item>
        <!-- Secondary brand color. -->
        <item name="colorSecondary">@color/black</item>
        <item name="colorSecondaryVariant">@color/black</item>
        <item name="colorOnSecondary">@color/black</item>
        <!-- Status bar color. -->
        <item name="android:statusBarColor">?attr/colorPrimaryVariant</item>
        <!-- Customize your theme here. -->
    </style>

    <style name="Button1">
        <item name="android:layout_width">75dp</item>
        <item name="android:layout_height">75dp</item>
        <item name="android:textStyle">bold</item>
        <item name="android:textSize">27dp</item>
        <item name="android:gravity">center</item>
        <item name="android:padding">10dp</item>
        <item name="android:layout_margin">10dp</item>
        <item name="android:background">@drawable/shape1</item>
    </style>

    <style name="Button2">
        <item name="android:layout_width">75dp</item>
        <item name="android:layout_height">75dp</item>
        <item name="android:textStyle">bold</item>
        <item name="android:textSize">27dp</item>
        <item name="android:gravity">center</item>
        <item name="android:padding">10dp</item>
        <item name="android:layout_margin">10dp</item>
        <item name="android:background">@drawable/shape2</item>
    </style>
</resources>

-----------------------------------------------------------
------------------------------------------------------------
------------------------------------------------------------


animation

vector_square - drawable
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:height="640dp"
    android:width="640dp"
    android:viewportHeight="600"
    android:viewportWidth="600">
    <group
        android:name="rotationSquare"
        android:pivotX="300.0"
        android:pivotY="300.0"
        android:rotation="45.0" > <!-- Set rotation to 0 to keep it as a square -->
        <path
            android:name="square"
            android:fillColor="#d3e39a"
            android:pathData="M300,0 L400,0 L400,200 L300,200 Z" /> <!-- Defines a square -->
    </group>
</vector>


vector_demo
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:height="640dp"
    android:width="640dp"
    android:viewportHeight="600"
    android:viewportWidth="600">
    <group
        android:name="rotationGroup"
        android:pivotX="300.0"
        android:pivotY="300.0"
        android:rotation="45.0" >
        <path
            android:name="v"
            android:fillColor="#9ac1e3"
            android:pathData="M300,140 l 0,-140 140,140 0,0 -140,70z" />
    </group>
</vector>

vector_circle
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:height="1280dp"
    android:width="1280dp"
    android:viewportHeight="600"
    android:viewportWidth="600">
    <group
        android:name="circleGroup"
        android:pivotX="300.0"
        android:pivotY="300.0"
        android:rotation="0.0">
        <path
            android:name="circle"
            android:fillColor="#e39a9c"
            android:pathData="M350,150 a50,50 0 1,0 150,0 a50,50 0 1,0 -150,0" />
        <!-- Larger circle with a radius of 50 -->
    </group>
</vector>


mainActivity.java: 
package com.example.graphics;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.view.ViewCompat;

import android.animation.Animator;
import android.animation.AnimatorSet;
import android.animation.ObjectAnimator;
import android.annotation.SuppressLint;
import android.content.res.ColorStateList;
import android.graphics.Color;
import android.graphics.drawable.Animatable2;
import android.graphics.drawable.AnimatedVectorDrawable;
import android.graphics.drawable.Drawable;
import android.os.Build;
import android.os.Bundle;
import android.os.Handler;
import android.view.GestureDetector;
import android.view.MotionEvent;
import android.view.View;
import android.view.animation.Animation;
import android.view.animation.AnimationSet;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.Toast;

import java.util.ArrayList;
import java.util.Random;

public class MainActivity extends AppCompatActivity {
    private View circularView;
    private GestureDetector gestureDetector;
    private Handler handler = new Handler();
    private Button btn;
    private ImageView imageView;
    private AnimatedVectorDrawable animatedVectorDrawable1,animatedVectorDrawable2,animatedVectorDrawable3;

    @SuppressLint("MissingInflatedId")
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        circularView = findViewById(R.id.circle);
        imageView=findViewById(R.id.imageAni);
        btn=findViewById(R.id.btn);

        animatedVectorDrawable1=(AnimatedVectorDrawable) getResources().getDrawable(R.drawable.animated_circle);
        animatedVectorDrawable2=(AnimatedVectorDrawable) getResources().getDrawable(R.drawable.animated_square);
        animatedVectorDrawable3=(AnimatedVectorDrawable) getResources().getDrawable(R.drawable.animated_demo);

        imageView.setImageDrawable(animatedVectorDrawable1);
        // Create a GestureDetector to detect double-taps
        gestureDetector = new GestureDetector(this, new GestureDetector.SimpleOnGestureListener() {
            @Override
            public boolean onDoubleTap(MotionEvent e) {
                int tintColor = generateRandomColor();
                ViewCompat.setBackgroundTintList(circularView, ColorStateList.valueOf(tintColor));
                return true;
            }
        });

        circularView.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View v, MotionEvent event) {
                // Pass touch events to the GestureDetector to handle double-tap
                gestureDetector.onTouchEvent(event);
                return true;
            }
        });
    }
    private void showToast(String message) {
        Toast.makeText(this, message, Toast.LENGTH_SHORT).show();
    }

    private int generateRandomColor() {
        Random random = new Random();
        int red = random.nextInt(256);
        int green = random.nextInt(256);
        int blue = random.nextInt(256);
        return Color.rgb(red, green, blue);
    }

    public void startAnimation(View view) {
        imageView.setVisibility(View.VISIBLE);
        circularView.setVisibility(View.INVISIBLE);

        // Start the animation
        handler.postDelayed(new Runnable() {
            @Override
            public void run() {
                if (animatedVectorDrawable1 != null) {
                    animatedVectorDrawable1.start();
                }
            }
        }, 0); // Delay of 0 milliseconds

        // Start the second animation after a delay
        handler.postDelayed(new Runnable() {
            @Override
            public void run() {
                imageView.setImageDrawable(animatedVectorDrawable2);
                if (animatedVectorDrawable2 != null) {
                    animatedVectorDrawable2.start();
                }
            }
        }, 6000); // Delay of 3000 milliseconds (3 seconds)

        // Start the third animation after a delay
        handler.postDelayed(new Runnable() {
            @Override
            public void run() {
                imageView.setImageDrawable(animatedVectorDrawable3);
                if (animatedVectorDrawable3 != null) {
                    animatedVectorDrawable3.start();
                }
            }
        }, 12000);

        handler.postDelayed(new Runnable() {
            @Override
            public void run() {
                imageView.setVisibility(View.INVISIBLE);
                circularView.setVisibility(View.VISIBLE);
            }
        }, 19000);
    }
}

Activity.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <View
        android:id="@+id/circle"
        android:layout_width="109dp"
        android:layout_height="97dp"
        android:layout_centerInParent="true"
        android:background="@drawable/circle_shape"
        app:layout_constraintBottom_toTopOf="@id/btn"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"

        app:layout_constraintTop_toBottomOf="@id/circle" />

    <Button
        android:id="@+id/btn"
        android:layout_width="177dp"
        android:layout_height="73dp"
        android:layout_marginBottom="208dp"
        android:backgroundTint="#e3bc9a"
        android:onClick="startAnimation"
        android:text="Graphics"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />

    <ImageView
        android:id="@+id/imageAni"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/vector_demo"
        android:visibility="invisible"
        app:layout_constraintBottom_toTopOf="@id/btn"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.867" />

</androidx.constraintlayout.widget.ConstraintLayout>

circle_shape - drawable
<shape xmlns:android="http://schemas.android.com/apk/res/android"  android:shape="rectangle">
    <solid android:color="#bc9ae3" />
    <size
        android:width="100dp"
        android:height="100dp" />
</shape>

animated_square - drawable
<animated-vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:drawable="@drawable/vector_square" >
    <target
        android:name="rotationSquare"
        android:animation="@animator/rotation" />
    <!--    <target-->
    <!--        android:name="v"-->
    <!--        android:animation="@animator/path_morph" />-->
</animated-vector>

animated_demo - drawable
<animated-vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:drawable="@drawable/vector_demo" >
    <target
        android:name="rotationGroup"
        android:animation="@animator/rotation" />
    <!--    <target-->
    <!--        android:name="v"-->
    <!--        android:animation="@animator/path_morph" />-->
</animated-vector>

animated_circle - drawable
  android:drawable="@drawable/vector_circle" >
    <target
        android:name="circleGroup"
        android:animation="@animator/rotation" />
    <!--    <target-->
    <!--        android:name="v"-->
    <!--        android:animation="@animator/path_morph" />-->
</animated-vector>

path_morph - animator - res
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <objectAnimator
        android:duration="3000"
        android:propertyName="pathData"
        android:valueFrom="M300,70 l 0,-70 70,70 0,0   -70,70z"
        android:valueTo="M300,70 l 0,-70 70,0  0,140 -70,0 z"
        android:valueType="pathType" />
</set>

rotation - res - animator
<objectAnimator android:duration="6000"
    android:propertyName="rotation"
    android:valueFrom="0"
    android:valueTo="360"
    xmlns:android="http://schemas.android.com/apk/res/android" />

-----------------------------------
-------------------------------------
-----------------------------------

package com.example.gps

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import android.Manifest;
import android.annotation.SuppressLint;
import android.content.pm.PackageManager;
import android.location.Location;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import com.google.android.gms.location.FusedLocationProviderClient;
import com.google.android.gms.location.LocationServices;
import com.google.android.gms.tasks.OnSuccessListener;

public class MainActivity extends AppCompatActivity {
    private static final int REQUEST_LOCATION_PERMISSION = 1;
    private FusedLocationProviderClient fusedLocationClient;
    private Button buttonGetLocation;
    private TextView textViewLatitude;
    private TextView textViewLongitude;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        fusedLocationClient = LocationServices.getFusedLocationProviderClient(this);

        buttonGetLocation = findViewById(R.id.buttonGetLocation);
        textViewLatitude = findViewById(R.id.textViewLatitude);
        textViewLongitude = findViewById(R.id.textViewLongitude);

        buttonGetLocation.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (ContextCompat.checkSelfPermission(MainActivity.this, Manifest.permission.ACCESS_FINE_LOCATION) == PackageManager.PERMISSION_GRANTED) {
                    // Permission is granted, fetch the location
                    fetchLocation();
                } else {
                    // Permission is not granted, request it
                    ActivityCompat.requestPermissions(MainActivity.this, new String[]{Manifest.permission.ACCESS_FINE_LOCATION}, REQUEST_LOCATION_PERMISSION);
                }
            }
        });
    }

    @SuppressLint("MissingPermission")
    private void fetchLocation() {
        fusedLocationClient.getLastLocation()
                .addOnSuccessListener(this, new OnSuccessListener<Location>() {
                    @Override
                    public void onSuccess(Location location) {
                        if (location != null) {
                            double latitude = location.getLatitude();
                            double longitude = location.getLongitude();
                            textViewLatitude.setText("Latitude: " + latitude);
                            textViewLongitude.setText("Longitude: " + longitude);
                        } else {
                            textViewLatitude.setText("Location not available");
                            textViewLongitude.setText("Location not available");
                        }
                    }
                });
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == REQUEST_LOCATION_PERMISSION) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                // Permission granted, fetch the location
                fetchLocation();
            } else {
                // Permission denied, handle it accordingly
            }
        }
    }
};

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">



        <TextView
            android:id="@+id/textViewLatitude"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Latitude"
            android:layout_centerHorizontal="true"

            android:layout_marginTop="16dp" />

        <TextView
            android:id="@+id/textViewLongitude"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Longitude"
            android:layout_centerHorizontal="true"
            android:layout_below="@id/textViewLatitude"
            android:layout_marginTop="16dp" />

        <Button
            android:id="@+id/buttonGetLocation"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@id/textViewLongitude"
            android:layout_gravity="center"
            android:layout_marginTop="29dp"
            android:layout_centerHorizontal="true"
            android:layout_centerVertical="true"
            android:text="Get Location" />
    </RelativeLayout>

</androidx.constraintlayout.widget.ConstraintLayout>

--------------------------------------
---------------------------------------
---------------------------------------
Light sensor 
package com.example.myapplication;

import androidx.appcompat.app.AppCompatActivity;

import android.app.Service;
import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity implements SensorEventListener {

    TextView light_text;
    TextView light_type;
    SensorManager sensorManager;
    Sensor sensor;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        light_text=findViewById(R.id.tv_text);
        light_type=findViewById(R.id.type_text);
        sensorManager= (SensorManager) getSystemService(Service.SENSOR_SERVICE);
        sensor=sensorManager.getDefaultSensor(Sensor.TYPE_LIGHT);

    }

    @Override
    protected void onPause(){
        super.onPause();
        sensorManager.unregisterListener(this);
    }

    @Override
    protected void onResume(){
        super.onResume();
        sensorManager.registerListener(this,sensor,SensorManager.SENSOR_DELAY_NORMAL);
    }
    @Override
    public void onSensorChanged(SensorEvent sensorEvent) {
        if(sensorEvent.sensor.getType()==Sensor.TYPE_LIGHT){
            String newText;
            if(sensorEvent.values[0]==0){
                newText="Pitch Black";
            }
            else if(sensorEvent.values[0]<10){
                newText="Dark";
            }
            else if(sensorEvent.values[0]<=10){
                newText="Dark";
            }
            else if(sensorEvent.values[0]<=50){
                newText="Grey";
            }
            else if(sensorEvent.values[0]<=5000){
                newText="Normal";
            }
            else if(sensorEvent.values[0]<=25000){
                newText="Incredibly Bright";
            }
            else{
                newText="This light will blind you";
            }

            light_text.setText(""+ sensorEvent.values[0]);
            light_type.setText(newText);
        }
    }

    @Override
    public void onAccuracyChanged(Sensor sensor, int i) {

    }
}
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/relativeLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/cardview_light_background"
    tools:context=".MainActivity">

    <!-- Textview to show light sensor reading -->
    <TextView
        android:id="@+id/type_text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_centerVertical="true"
        android:layout_marginTop="128dp"
        android:text="Brightness"
        android:textColor="@color/black"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/tv_text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_centerVertical="true"
        android:text="Light Sensor"
        android:textColor="@color/black"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>

---------------------------------------
-----------------------------------------
----------------------------------------

QR code

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="@color/nude"
        android:text="Camera"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.847" />
</androidx.constraintlayout.widget.ConstraintLayout>

package com.example.qrcode;

import static android.app.ProgressDialog.show;

import androidx.appcompat.app.AppCompatActivity;

import android.content.ClipData;
import android.content.ClipboardManager;
import android.content.Context;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

import com.google.zxing.integration.android.IntentIntegrator;
import com.google.zxing.integration.android.IntentResult;

public class MainActivity extends AppCompatActivity {
    private Button btn;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        btn=findViewById(R.id.button);
        btn.setOnClickListener(new View.OnClickListener() {

            public void onClick(View v) {

                new IntentIntegrator(MainActivity.this).initiateScan();

            }

        });
    }

    @Override

    protected void onActivityResult(int requestCode, int resultCode, Intent data) {

        IntentResult result = IntentIntegrator.parseActivityResult(requestCode, resultCode, data);

        if(result != null) {

            if(result.getContents() == null) {

                Toast.makeText(this,"Scan Cancelled", Toast.LENGTH_LONG).show();

            } else {

                Toast.makeText(this, "Scanned" + result.getContents(), Toast.LENGTH_LONG).show();
                ClipboardManager clipboard = (ClipboardManager)
                        getSystemService(Context.CLIPBOARD_SERVICE);
                ClipData clip = ClipData.newPlainText("Intent", result.getContents());
                clipboard.setPrimaryClip(clip);
            }

        } else {

            super.onActivityResult(requestCode, resultCode, data);

        }

    }
}
-------------------------------------
---------------------------------------
-----------------------------------------

change text size

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp"
    android:gravity="center"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/editText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter text"
        android:layout_marginBottom="16dp"/>

    <Button
        android:id="@+id/changeSizeButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Change Text Size"
        android:onClick="changeTextSize"
        android:layout_gravity="center"/>

    <TextView
        android:id="@+id/displayTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text=""
        android:layout_gravity="center"
        android:layout_marginTop="16dp"
        android:textSize="20sp"/>

</LinearLayout>

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private EditText editText;
    private TextView displayTextView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editText = findViewById(R.id.editText);
        displayTextView = findViewById(R.id.displayTextView);
    }

    public void changeTextSize(View view) {
        String inputText = editText.getText().toString();
        int textSize = 20; // Default text size in sp

        try {
            textSize = Integer.parseInt(inputText);
        } catch (NumberFormatException e) {
            // Handle invalid input (e.g., non-integer input)
        }

        displayTextView.setTextSize(textSize);
    }
}
-------------------------------------
------------------------------------
-------------------------------------

ATS calculator

package com.example.atscalculator;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.app.NotificationCompat;
import androidx.core.app.NotificationManagerCompat;
import android.annotation.SuppressLint;
import android.content.pm.PackageManager;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;
public class MainActivity extends AppCompatActivity implements 
View.OnClickListener {
 Button buttonAdd, buttonSub, buttonMul, buttonDiv, notifybtn;
 EditText editTextN1, editTextN2;
 TextView textView;
 int num1, num2;
 @Override
 protected void onCreate(Bundle savedInstanceState) {
 super.onCreate(savedInstanceState);
 setContentView(R.layout.activity_main);
 buttonAdd = findViewById(R.id.btn_add);
 buttonSub = findViewById(R.id.btn_sub);
 buttonMul = findViewById(R.id.btn_mul);
 buttonDiv = findViewById(R.id.btn_div);
 editTextN1 = findViewById(R.id.number1);
 editTextN2 = findViewById(R.id.number2);
 textView = findViewById(R.id.result);
 notifybtn = findViewById(R.id.btn_notify);
 buttonAdd.setOnClickListener(this::onClick);
 buttonSub.setOnClickListener(this::onClick);
 buttonMul.setOnClickListener(this::onClick);
 buttonDiv.setOnClickListener(this::onClick);
 notifybtn.setOnClickListener(new View.OnClickListener() {
 @SuppressLint("MissingPermission")
 @Override
 public void onClick(View view) {
 NotificationCompat.Builder builder = new 
NotificationCompat.Builder(MainActivity.this, "My Notification");
builder.setContentTitle("Ats Calculator");
 builder.setContentText("Result"+textView.getText().toString());
 builder.setSmallIcon(R.drawable.ic_launcher_background);
 builder.setAutoCancel(true);
 NotificationManagerCompat managerCompat = 
NotificationManagerCompat.from(MainActivity.this);
 managerCompat.notify(1, builder.build());
 }
 });
 }
 public int getIntFromEditText(EditText editText) {
 if (editText.getText().toString().equals("")) {
 Toast.makeText(this, "Enter Valid number", 
Toast.LENGTH_SHORT).show();
 return 0;
 } else
 return Integer.parseInt(editText.getText().toString());
 }
 @Override
 public void onClick(View view) {
 num1 = getIntFromEditText(editTextN1);
 num2 = getIntFromEditText(editTextN2);
 int id = view.getId();
 if (id == R.id.btn_add) {
 textView.setText("Answer = " + (num1 + num2));
 } else if (id == R.id.btn_sub) {
 textView.setText("Answer = " + (num1 - num2));
 } else if (id == R.id.btn_mul) {
 textView.setText("Answer = " + (num1 * num2));
 } else if (id == R.id.btn_div) {
textView.setText("Answer = " + ((float) num1 / (float) num2));
 }
 }
}


<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
 xmlns:app="http://schemas.android.com/apk/res-auto"
 xmlns:tools="http://schemas.android.com/tools"
 android:layout_width="match_parent"
 android:layout_height="match_parent"
 android:orientation="vertical"
 android:padding="20dp"
 tools:context=".MainActivity">
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:text="ATS Calculator"
 android:textSize="30sp"
 android:textStyle="bold"
 android:layout_marginTop="50dp"
 android:layout_gravity="center"
 />
 <EditText
 android:id="@+id/number1"
 android:layout_width="match_parent"
 android:layout_height="wrap_content"
 android:layout_marginTop="30dp"
 android:hint="Enter Number 1 :"
 android:inputType="number"
 />
<EditText
 android:id="@+id/number2"
 android:layout_width="match_parent"
 android:layout_height="wrap_content"
 android:layout_marginTop="10dp"
 android:hint="Enter Number 2 :"
 android:inputType="number"
 />
 <LinearLayout
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:orientation="horizontal">
 <Button
 android:id="@+id/btn_add"
 style="@style/Widget.AppCompat.Button.Colored"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_marginEnd="5dp"
 android:text="+"
 android:textSize="30sp" />
 <Button
 android:id="@+id/btn_sub"
 style="@style/Widget.AppCompat.Button.Colored"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_marginEnd="5dp"
 android:text="-"
 android:textSize="30sp" />
 <Button
 android:id="@+id/btn_mul"
 style="@style/Widget.AppCompat.Button.Colored"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
android:layout_marginEnd="5dp"
 android:text="*"
 android:textSize="30sp" />
 <Button
 android:id="@+id/btn_div"
 style="@style/Widget.AppCompat.Button.Colored"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_marginEnd="5dp"
 android:text="/"
 android:textSize="30sp" />
 </LinearLayout>
 <TextView
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:id="@+id/result"
 android:layout_gravity="center"
 android:textSize="30sp"
 android:textStyle="bold"
 android:layout_marginTop="30dp"/>
 <Button
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_gravity="center"
 android:text="Get Notified"
 android:textSize="15dp"
 android:id="@+id/btn_notify"
 />
</LinearLayout>

-------------------------------
---------------------------------
--------------------------------

change colour

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@android:color/white"
    tools:context=".MainActivity">

    <ImageView
        android:id="@+id/shapeImageView"
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:layout_centerInParent="true"
        android:src="@drawable/circle_shape"
        android:clickable="true"
        android:onClick="changeShapeColor"
        android:background="?attr/selectableItemBackgroundBorderless"/>

</RelativeLayout>

drawable - circle_Shape

<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <solid android:color="#FF5733"/> <!-- Initial color -->
</shape>

MainACtivity.java
import android.graphics.drawable.ColorDrawable;
import android.os.Bundle;
import android.view.View;
import android.widget.ImageView;

import androidx.annotation.ColorInt;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private ImageView shapeImageView;
    private int[] colors = {0xFF5733, 0xFFC300, 0xFF5733}; // Colors to cycle through
    private int colorIndex = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        shapeImageView = findViewById(R.id.shapeImageView);
    }

    public void changeShapeColor(View view) {
        if (colorIndex < colors.length - 1) {
            colorIndex++;
        } else {
            colorIndex = 0;
        }

        @ColorInt int newColor = colors[colorIndex];
        shapeImageView.setImageDrawable(new ColorDrawable(newColor));
    }
}

----------------------------------
------------------------------------
----------------------------------

change shape 

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp"
    tools:context=".MainActivity">

    <View
        android:id="@+id/shapeView"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@drawable/circle_shape"
        android:layout_centerInParent="true"
        android:clickable="true"
        android:focusable="true"
        android:onClick="changeShapeOnClick" />

</RelativeLayout>

drawable 
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <solid android:color="#FF0000" /> <!-- Red circle -->
</shape>

<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="#00FF00" /> <!-- Green rectangle -->
</shape>
MainACtivity.java
package com.example.shapechanger;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private boolean isCircle = true;
    private View shapeView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        shapeView = findViewById(R.id.shapeView);
    }

    public void changeShapeOnClick(View view) {
        if (isCircle) {
            shapeView.setBackgroundResource(R.drawable.rectangle_shape);
        } else {
            shapeView.setBackgroundResource(R.drawable.circle_shape);
        }
        isCircle = !isCircle;
    }
}

