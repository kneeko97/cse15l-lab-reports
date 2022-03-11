# Week 8: Lab Report 4
 
## Markdown Snippets

---
**My Group's Repository:**

1. [Link to our repository](https://github.com/kneeko97/markdown-parse.git)
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
5. For snippet2, I used jdb for detailed line-by-line debugging. It appears that my implementation does not
recognize that "backslash[" and "backslash]" are characters rather than open and closed brackets. I believe I could fix this issue in less than 10 lines of code. I would need to check whether my open and closed brackets have a backslash infront of their them. If they do, then I would not consider them as nextOpenBracket or nextCloseBracket and rather continue my search after that index. 
6. Snippet3 requires no changes to the code.


**Other Group's Repository**
1. [Link to their repository](https://github.com/atruong39/markdown-parse.git)

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
4. Unfortunately, I am not knowledgable on String regex and do not know how to fix the following code: 
    ```
    ArrayList<String> toReturn = new ArrayList<>();
        String regex = "(?<!!)\\[.+\\]\\(\\h*(\\S+)\\h*\\)";
        Matcher matcher = Pattern.compile(regex).matcher(markdown);

        while(matcher.find()) {
            toReturn.add(matcher.group(1).replaceAll(" ", ""));
        }

        return toReturn;
    ```
    I'm certain that the original author of the code could fix all failed snippet tests in less than 10 lines. They could potentially even fix it in a few lines total. However, if I were to fix the issues it would require significantly more than 10 lines because I would have to implement all of the code from our more typical approach.

    From the failure output, I noticed that their program extracted 4 links from snippet 1 whereas mine only extracted 3. So, it appears that the their code is successful in finding links given a target syntax. However, they would need to add further restirctions to limit how many links should be extracted. The same sentiment applies to fixing the issues in snippet2.

    Interestingly, for snippet3, it did not register any links. I assume this is because this snippet included examples that significatly differed from the target syntax of proper links.