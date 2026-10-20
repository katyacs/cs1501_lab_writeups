# Lab 3 Write-Up

## Code

```java
public class LZW {
    private static final int R = 256; // number of input chars
    private static int L = 512; // number of codewords = 2^W
    private static int W = 9; // codeword width

    public static void compress() {
        L = 512;
        W = 9;
        String input = BinaryStdIn.readString();
        TST<Integer> st = new TST<Integer>();
        for (int i = 0; i < R; i++)
            st.put("" + (char) i, i);
        int code = R + 1; // R is codeword for EOF
        while (input.length() > 0) {
            String s = st.longestPrefixOf(input); // Find max prefix match s.
            
            //added: 
            if(W < 16 && code > L)
            {
                L = L*2;
                W++;
            }

            BinaryStdOut.write(st.get(s), W); // Print s's encoding.
            int t = s.length();

            //changed: code < L to code < 2^16
            if (t < input.length() && code < 65536) // Add s to symbol table. 
                st.put(input.substring(0, t + 1), code++);
            input = input.substring(t); // Scan past s in input.
        }
        BinaryStdOut.write(R, W);
        BinaryStdOut.close();
    }

    public static void expand() {
       //added:
        W = 9;
        L = 512;

        //changed: instead of L, 2^16
        String[] st = new String[65536];
        
        int i; // next available codeword value

        // initialize symbol table with all 1-character strings
        for (i = 0; i < R; i++)
            st[i] = "" + (char) i;
        st[i++] = ""; // (unused) lookahead for EOF

        int codeword = BinaryStdIn.readInt(W);
        if (codeword == R)
            return; // expanded message is empty string
        
        
        String val = st[codeword];

        while (true) {
            BinaryStdOut.write(val);

            //added: 
            if(W < 16 && i+1 > L)
            {
                L = L*2;
                W++;
            }
            codeword = BinaryStdIn.readInt(W);
            if (codeword == R)
                break;
            String s = st[codeword];
            if (i == codeword)
                s = val + val.charAt(0); // special case hack
            if (i < 65536)
                st[i++] = val + s.charAt(0);
            val = s;
        }
        BinaryStdOut.close();
    }
}
```
## Description
For this problem, you needed to take a fixed length LZW compression and make a variable width version that grows between 9 and 16 bits.
I made W (width of the codeword) and L(2^W) not final variables, so they could be reassigned during the compression and expansion functions.
At the start of each function I set L back to 512 and W back to 9.

In compress, before writing each codeword, I check if the newest entry fits in W bits and if it doesn't I double L and increment W.
Also, the dictionary stops growing at 2^16 (65536) instead of L.

In expand, I made the string array the max possible size of 2^16. It also checks if the next codeword will fit into W bits and if it doesn't, then increment W and double L.
It checks the next codeword and not the current codeword because expansion is always one entry behind the compressor. 

## Complexity Analysis
### Time
compress() should be O(n^2) because `.substring(t)` copies all of the remaining input.
expand() is O(n) because each loop does work equivalent to the number of characters in the string, so each character is processed about once.
### Space
compress() is O(n) for the input plus the TST with 2^16 entries, which is constant.
expand() is also O(n) because I created an array with a size of 65,536 references and the amount of strings stored in it should add up to about n characters.
