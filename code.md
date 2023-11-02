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
-----------------------