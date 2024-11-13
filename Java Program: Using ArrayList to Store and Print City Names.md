import java.util.ArrayList;

public class Solution {

    public static void main(String[] args) {
        ArrayList<String> a = new ArrayList<String>(); // Create an ArrayList to store city names
        a.add("GOA");      // Add "GOA" to the ArrayList
        a.add("Mumbai");   // Add "Mumbai" to the ArrayList
        for (String s : a) { // Enhanced for-loop to print each element
            System.out.println(s);
        }
    }
}
