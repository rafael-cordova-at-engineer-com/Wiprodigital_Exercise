Single Domain Simple Web Crawler Program
=======

## Notes:
* The fact that I am very thorough and pay attention to details and the fact that I currently have limited access to computer forced me to limit how much to produce for this exercise.
  I would have enjoyed making it full proof with all pertinent documentation but then it would have become too large for the intention of the exercise.

* Made as prototype with enough written details to facilitate discussions and tradeoff analyses.

* With this prototype, I can demonstrate and justify every item in a discussion.

* In practice, I would have contacted users and derived a more exhaustive list of requirements.
  For this exercise the approach taken was to make my own considerations and decisions
  in order to facilitate knowlwdge gathering and analyses before commiting to a full
  development effort.

## Considerations made:
  1. Multiple uses for the crawlwer that affects design and implementation
    * to find broken and missing links within own web site
    * to discover content in someone else's web site
    * to create indeces for future searches
  2. Multiple clients and users
    * write reference program for internal use 
      and modify client's version to fit clients computing environment
      * polyglot: 
        1. write to minimize changes for deployed versions
        2. use of std practice versus customized algorithms for efficiency and performance

## Decisions made:
  1. uses Java as it has become the most common language and VM of choice for large corporations
     * Java can be translated to C# for small businesess that uses Microsoft
  2. The maion design is procedural to
     * facilitate translation to C/C++ and other lambda languages, i.e LISP
     * avoid unnecessary Object processing overhead by the VM
     * OO can be added if creating web site graphs and for graphical representations
     * made initial modularization of functions that can be used in multiple systems
  3. Made attempt to validate hyperlinks but the nature of text authoring and that fact that there are a large amount of permutations of ways to wrute HTML code that the program was written with the main assumption that links and HTML content is valid.
     Some source code was written toward upgrading but it was left commented out and marked with as 'TO DO:'
  4. Output is via console at the moment but can be upgraded with a very small amount of source code deletions
  5. Testing was separated as UNIT, Integration and System
     * System testing were performed via Eclipse IDE
     * Unit and Integration testing were performed via JUnit functins
     * JUnit functions were marked by pepending name with 'Unit' or 'Intg'to facilitate readability
     * There is a one-to-one relation within the JUnit and operational functions
       Separation of test case type was started but left commented out and marked with 'To DO:'
  6. A particular function passes Unit Tests and the logic was verified to be correct but there is a failure in the live test
     debugging of the failure in live testing found that a particular link (the 24th in the content) causes program control to branch to the incorrect code block
     I personaly has seen this once in my career and the probable cause is in the input data (probably a hidden character)
     Another possible cause is an badly produced program from the compiler, i.e. via optimization
     This will require more time to investigate.
  7. Comments and documentation are highly desired but not everyone practices it.
     I made an attempt to just write few comments instead of my approach to document first and the write source code
     I also used TDD and BDD approach were tests are written first and hence most comments are in the test function descriptin block as it serves as the entry point for reading
  8. The crawl algorithm was made recursive for development time consideration and as temporary
     No exit condition source code
     A live test showed over 460 invokations without crashing
     Must be replaced withb an iterative, preferably a graph algorithm
  9. Ommitted query string on URI
 10. Omitted processing of port numbers in host spec of URL
 11. Use of class String, which is very inneficient but it is the std  practice
 12. Uploaded eclipse workspace on a zip file for convenience
 13. System Tests were performed via output inspection and debugging.
     This approach necessitates written procedures, which were not written due to time constraint
     This can also be skipped and instead JUnit test cases can be written to read test input data from files
     and to evaluate conditions via results written into files.

## Things to do with more time alloted:
  1. Write full descriptions in source code
  2. Write web site map with a graph data representation and algorithm
  3. Write full validation of hyperlinks and web content
  4. Add input and output to/from files
  5. Write JUnit functions for file I?O system tests
  6. Add processing of ommited items listed in the decisiopn section
  7. Process hyperlinks in xml content found
     i.e. 'path=...", <...Link>hyperlink>, etc
  8. Create a project structure in the repository


## Best Practices:
  My best practices are to based on concepts and being able to perform tasks and not based on published books.
  They are manifested different depending on the project.
  They are as follow:
  * Add references to requirements in source code.
  * Provide clear and complete descriptions to every module, every file and every class.
  * Annotate source code with short statements indicating what the source code is to do
  * Write self documenting source code as much as possible
  * Write references to every module to provide traceability and facilitate source code modifications without creating new defects

 ## Testing:
  * Provide multiple ways to invoke tests, i.e. by modules, by particular categories
  * Tests Units as Black Box Testing
  * Test Integration via White Box Testing
  * Test System via White Box Testing
  * Perfom full regression testing before committing changes


##  Program description (to be added withon source code when time permits)
  The SimpleWebCrawler program accepts a hyperlink and crawls to all discovered web pages within the domain of the provided root hyperlink.
  Web content is not validated and it is processed in top down order, skipping any content that is not of interest.
  Discovered links are maintain in a set (no duplicates) to prevent repeated processing of web pages.
  For all web pages, after processing its content and discovering links, a list of hyperlinks found are displayed in the screen and categorized as web pages, images, anchors and scripts.
  After displaying found links then the crawler iterates a search on the found web pages in the order in which they were found, the same order in which they appear in the web page.  
  Crawling was implemented using recursion and it traverses web pages in a depth first fashion.  
  After all web pages are processed the program displays the total amount of links found and list them in order of discovery.

### Program Structure:
  The program is partitioned into crawling function and a set of utilites modules that can be used by multiple modules and even multiple projects.
  The crawling modules and their associated tests are separated in different packages in order to deploy the crawling function into other programs without having to import tests.
  Crawling logic is devided into the main module and a module class that perfroms the crawling function.
  For simplicity, methods to provide content from unsecured, secured web pages and local files are provided.
  These functions are to be moved to a common package to be shared with other programs at some future.
  At the moment are customized for the crawlwer. They take an URI, open any connection or infracstructure operations and read content.



## Installation and Build Instructions:
  * Get Java Java SE 11.0.1(LTS)
    From https://www.oracle.com/technetwork/java/javase/downloads/index.html

    Click on : Java SE 11.0.1(LTS) -
    https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html

    Accept License Agreement
    Click On Link: jdk-11.0.1_windows-x64_bin.exe
    Save File: jdk-11.0.1_windows-x64_bin.exe
    Double Click on file: jdk-11.0.1_windows-x64_bin


  * Get Eclipse IDE 2018-09
    From https://www.eclipse.org/downloads/
    https://www.eclipse.org/downloads/download.php?file=/oomph/epp/2018-09/Ra/eclipse-inst-win64.exe
    
    If pop up window comes up and ask to find Java, then click on the YES button.
    Choose: Eclipse IDE for Java Developers

    Altyernate or errors in link then 
    open file: ...\workspace_java_WiproDigital\SimpleWebCrawlerInstructions_unicode.txt




## Requirements List:  
1. Simple
2. The crawler should be limited to one domain
3. Given a starting URL, it should visit all pages within the source URL's domain
4. The output should be a simple structured site map
5. For all visited pages show their included links to other pages under the same domain
6. For all visited pages show their included links to other pages to external domains
7. For all visited pages show their included links to static content



## Design Whiteboard:

### Design

#### Languages:
      PERL, Python and other scripting languages
      built in pattern matching functions


#### Passing Data
  * Utility style - Pass Lists to append
      can be shared across different implementations, even OO
  * Self Contained - append what is returned
     module sets 


#### Issues:
  1. Memory allocation
  2. Handling out of memory conditions

  3. Procedure/Functional design 
     * is the simplest
     * most reuse - units can be independent of  
     * less memory
     * less overhead than Objects
     * designs can be implemented inj other languages without design modification
  4. Object Oriented
     * very elegant and expressive
     * can encapsulate data
     * facilitate multiple output formats
     * create networks, useful for graphical representation of output
  5. Lambda
     * LISP
     * few people knows how to program
     * dynamic
     * can be fed to AI systems written in LISP
