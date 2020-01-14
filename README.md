# tokenizer-class

import java.util.*;
import java.io.*;

/**
 * Tokenizer serves as an implementation of the StringTokenizer class
 * built into Java. It parses a given file into individual Tokens and stores
 * these individual Tokens throughout.
 *
 * @author Asma Awad
 * @version 1.0
 */
public class Tokenizer {

    private ArrayList<Token> tokens;
    private int count = 0; //keeps track of the Token being looked at

    Tokenizer(String filename) throws IOException {
        tokens = new ArrayList<>();
        //open the file
        Scanner infile = new Scanner(new File(filename));
        StringBuilder str = new StringBuilder();

        //put each word from the file into a single string
        while (infile.hasNext()) {
            str.append(infile.next()).append(" ");
        }
        //split the string by spaces, and add each word into an array
        String[] words = str.toString().split(" ");

        //add each word of the array into the ArrayList as Tokens as opposed to Strings
        for (int i = 0; i < words.length; i++) {
            tokens.add(new Token(filename, words[i], i));
        }
    }

    /**
     * next provides the next Token to be looked at in a list of Tokens created through the Tokenizer
     * @return the next Token that has not yet been looked at
     */
    public Token next() {
        //save the current Token value at count's value
        Token t = tokens.get(count);
        //increment count for when next is called again in order to return the next Token
        count++;
        return t;
    }

    /**
     * hasNext determines whether or not there are more Tokens to be looked at
     * @return true if there are more Tokens to be traversed, and false otherwise
     */
    public boolean hasNext() {
        //if count represents an index that's out of bounds
        if (count >= tokens.size())
            return false;
        return true;
    }
}
