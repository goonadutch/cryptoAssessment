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
----------------RSA----------

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
------------------
