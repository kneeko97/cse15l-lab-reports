# Week 8: Lab Report 4
 
## Markdown Snippets

---
**Repositories:**

1. [My Repository](https://github.com/kneeko97/markdown-parse.git)
2. [Other Group  Repository](https://github.com/atruong39/markdown-parse/blob/main/MarkdownParse.javae)

**MarkdownParseTest.java**

1. First, lets look at my implementation for adding snippet tests. 
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
My snippet3 test passed but the first two failed. Lets take a look at the test failure output.
![snippet1 and snippet2 failure](mySnippetFailure.png)


2. Second, I used the same implementation for the other groups MarkdownParseTest.java file
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
None of their tests passed. Lets take a look at the test failure output.
![snippet1, snippet2, and snippet3 failure message](otherSnippetFailure.png)
