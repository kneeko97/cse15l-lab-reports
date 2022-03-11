# Week 8: Lab Report 4
 
## Markdown Snippets

---
**My Repositories:**

1. [My Repository](https://github.com/kneeko97/markdown-parse.git)
2. First, lets look at my implementation for adding the snippet tests. 
    ```
    @Test 
    public void snippet1() throws IOException{
        String contents = Files.readString(Path.of("./snippet1.md"));
        List<String> expect = List.of("`google.com");
        assertEquals(expect, MarkdownParse.getLinks(contents));
    }

    @Test
    public void snippet2() throws IOException{
        String contents = Files.readString(Path.of("./snippet2.md"));
        List<String> expect = List.of("a.com", "a.com((", "example.com");
        assertEquals(expect, MarkdownParse.getLinks(contents));
    }

    @Test
    public void snippet3() throws IOException{
        String contents = Files.readString(Path.of("./snippet3.md"));
        List<String> expect = List.of("https://www.twitter.com", "https://ucsd-cse15l-w22.github.io/");
        assertEquals(expect, MarkdownParse.getLinks(contents));
    }
    ```
3. My snippet3 test passed but the first two failed. Lets take a look at the test failure output.
    ![snippet1 and snippet2 failure](mySnippetFailure.png)
4. For snippet1, I can fix the failed tests in less than 10 lines of code. I would have to implement two additional if statements that check for '`' occuring before or after nextOpenBracket. Check the code before for reference.
    ```
    if(markdown.charAt(nextOpenBracket +1) == '`'){
        currentIndex = closeParen +1;
        continue;
    }
    if(nextOpenBracket != 0 && markdown.charAt(nextOpenBracket - 1) == '`'){
        currentIndex = closeParen +1;
        continue;
    }
    ```
5. For snippet2, I used jdb for detailed line-by-line debugging. It appears that the last link is not read as a proper link because my program checks  whether there is a openParen directly after the nextCloseBracket. Since this example does not fit that condition, the link is tossed aside. It seems possible to fix the issue in less than 10 lines of code. I would suggest having a counter for how many nextOpenBrackets and nextClosedBrackets exist. Then we would want to use the first instance of nextOpenBracket and last instance of nextCloseBracket as our correct format. Then we could effectively our current checker on whether the character after nextCloseBracket is an openParen or not. 

6. Snippet3 requires no changes to the code.


**Other Group Repository**
1. [Their repository link](https://github.com/atruong39/markdown-parse.git)

2. I used the same implementation for the other groups MarkdownParseTest.java file
    ```
    @Test 
    public void snippet1() throws IOException{
        String contents = Files.readString(Path.of("./snippet1.md"));
        List<String> expect = List.of("`google.com");
        assertEquals(expect, MarkdownParse.getLinks(contents));
    }

    @Test
    public void snippet2() throws IOException{
        String contents = Files.readString(Path.of("./snippet2.md"));
        List<String> expect = List.of("a.com", "a.com((", "example.com");
        assertEquals(expect, MarkdownParse.getLinks(contents));
    }

    @Test
    public void snippet3() throws IOException{
        String contents = Files.readString(Path.of("./snippet3.md"));
        List<String> expect = List.of("https://www.twitter.com", "https://ucsd-cse15l-w22.github.io/");
        assertEquals(expect, MarkdownParse.getLinks(contents));
    }
    ```
3. None of their tests passed. Lets take a look at the test failure output.
    ![snippet1, snippet2, and snippet3 failure message](otherSnippetFailure.png)
4.
5.
6. 