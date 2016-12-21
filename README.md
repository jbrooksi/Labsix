# Labsix
import java.util.Scanner;

public class labSix{

	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		System.out.println("Welcome to the Pig Latin Translation!");

		while (true) {
			System.out.print("Enter a line to be translated: ");
			String line = scan.nextLine();
			
			System.out.println("\n" + translate(line) + "\n");
			
			System.out.print("Translate another line (y/n)? ");
			String answer = scan.nextLine();
			char firstLetter = answer.toUpperCase().charAt(0);
			if (firstLetter == 'n' || firstLetter == 'N') {
				System.out.println("See you next time!");
				break;
			}
		}
		scan.close();
	}

	public static String translate(String line) {
		String translation = "";
		
		while (line.length() > 0) {
			//get rid of leading/trailing spaces
			//included inside loop in case there are double (or more) spaces inside line
			line = line.trim(); 

			String word;
			int firstSpace = line.indexOf(' ');
			if (firstSpace > 0) {
				word = line.substring (0, firstSpace); //from beginning until (not including) space
				line = line.substring (firstSpace + 1); //char after space until end
			} else {
				word = line;
				line = "";
			}
			if (translation.length() > 0)
				translation += " ";//add space between words
			translation += translateWord(word);
		}
		return translation;
	}
	
	private static String translateWord (String word){
		String newWord;
		
		int vowel = findVowel(word);
		if (vowel < 0){
			newWord = "{untranslatable}" + word;
		} else if (vowel == 0) {
			newWord = word + "way";
		} else {
			newWord = word.substring(vowel) + word.substring(0, vowel) + "ay";
		}
		
		newWord = fixCase (newWord, word);
		
		return newWord;
	}
	
	private static int findVowel (String word) {
		for (int i = 0; i < word.length(); i++){
			char letter = word.toLowerCase().charAt(i);
			if (letter == 'a' || letter == 'e' || letter == 'i' || letter == 'o' || letter == 'u')
				return i;
		}
		return -1;
	}
	
	public static String fixCase (String newWord, String word) {
		//original word is all upper case
		if (word.toUpperCase().equals(word)) 
			//return newWord as all upper
			return newWord.toUpperCase();
		
		//original word is all lower case
		if (word.toLowerCase().equals(word))
			//return newWord, which is already all lower
			return newWord;
		
		//if we got here, we're assuming Title Case
		//reality may be more complex
		String first = newWord.substring(0,1);
		first = first.toUpperCase();
		String rest = newWord.substring(1);
		rest = rest.toLowerCase();
		return first + rest;
	}
}
