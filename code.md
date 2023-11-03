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
------------------------------


