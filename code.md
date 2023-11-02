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
---------------------------