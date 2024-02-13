# Lab 3: Bugs and Commands (Week 5)
Caitlin McCallum
## Part 1: Bugs

### Failure Inducing Input

#### i. Junit - ArrayTests.java
```
  @Test 
	public void testReverseInPlace2() {
    int[] input1 = { 3, 2, 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{1, 2, 3}, input1);
}
```
#### ii. Associated Code - ArrayExamples.java
```
    1   static void reverseInPlace(int[] arr) {
    2       for(int i = 0; i < arr.length; i += 1) {
    3           arr[i] = arr[arr.length - i - 1];
    4       }
    5   }
```
### Successful Input
#### i. Junit - ArrayTests.java
```
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
 ```
#### ii. Associated Code - ArrayExamples.java
```
    1   static void reverseInPlace(int[] arr) {
    2       for(int i = 0; i < arr.length; i += 1) {
    3           arr[i] = arr[arr.length - i - 1];
    4       }
    5   }
```
### The Symptom
![Image](symptom.png)

### The Bug
#### Code Before: 
```
    1   static void reverseInPlace(int[] arr) {
    2	    for(int i = 0; i < arr.length; i += 1) {
    3	        arr[i] = arr[arr.length - i - 1];
    4	}
```
#### Code After: 
```
    1   static void reverseInPlace(int[] arr) {
    2	    int[] tempArray = new int[arr.length];
    3	    for(int i = 0; i < arr.length; i += 1) {
    4	        tempArray[i] = arr[arr.length - i - 1];
    5	    }
    6	    for(int i = 0; i < arr.length; i += 1) {
    7	        arr[i] = tempArray[i];
    8	    }
    9   }   
```
Fixes: During the initial for loop on line 3, the element to be reversed is placed in a new array `tempArray`, then copied back over to the original array in the second for loop on line 6 in order to not overwrite the elements.

## Part 2: Researching the Grep Command
### `-i`: Ignore Case
#### Example 1:
```
Caitlins-MBP:Media caitimccallum$ grep 'legal'  Farm_workers.txt 
Caitlins-MBP:Media caitimccallum$ grep -i 'legal' Farm_workers.txt
Report: Farm workers plagued by pesticides Legal aid group
A new study by Colorado Legal Services, the first of its kind in
Nevertheless, Chavez took her case to Colorado Legal Services, a
Legal Services, which reports that migrant workers at farms
Legal Services conducted interviews with 88 farm workers in some
Kimi Jackson, author of the Colorado Legal Services study, said
Yet the Legal Services report faults growers, farm-labor
Chavez said she called Colorado Legal Services because she felt
Caitlins-MBP:Media caitimccallum$
```
In this example I use the command line option -i for grep in order to display all instances of the word 'legal' regardless of case. As shown, when I ran the grep command without the -i command line option, there was no match found for 'legal' in the file since it only appears as 'Legal'. This could be useful for searching for a keyword in a file that may or may not have case differences. 

source: https://docs.rackspace.com/docs/use-the-linux-grep-command
#### Example 2:
```
Caitlins-MBP:Media caitimccallum$ grep 'poor' Advocate_for_Poor.txt 
helping East New York's poor, he's getting booted from the bodega
helping the working poor navigate the legal system. Immigration,
Caitlins-MBP:Media caitimccallum$ grep -i 'poor' Advocate_for_Poor.txt 
Advocate for Poor Has Own Obstacles
helping East New York's poor, he's getting booted from the bodega
helping the working poor navigate the legal system. Immigration,
Caitlins-MBP:Media caitimccallum$ 
```
In this example I use the command line option -i for grep in order to display all instances of the word 'poor' in the file Advocate_for_Poor.txt. When I ran grep originally without -i, there were only 2 lines found within the file that contained the word 'poor', this excluded the title line in which 'poor' is capitalized. This could be useful for if I was searching for a keyword in a file and also wanted to include the title of the text within the file which is often capitalized. 
source: https://docs.rackspace.com/docs/use-the-linux-grep-command

### `-c`: Print Number of Line Matches
#### Example 1:
```
Caitlins-MBP:Media caitimccallum$ grep -c 'legal' Farm_workers.txt
0
Caitlins-MBP:Media caitimccallum$ grep -ci 'legal' Farm_workers.txt
8
```
Using the same file as the example above, I can demonstrate how the -c and -i commands can work in conjunction to display a more easily read output. As shown before, when -i is not called with grep when looking for 'legal' in Farm_workers.txt, I get zero matches. Now rather than counting each line of output, which could be expansive, I can use -c command line option to quickly and easily count the number of matches.

source: https://docs.rackspace.com/docs/use-the-linux-grep-command
#### Example 2:
```
Caitlins-MBP:Media caitimccallum$ grep -c 'a' A_helping_hand.txt 
119
```
In this example, I'm looking for an extremely common word in A_helping_hand.txt. If I were to just use the grep command without -c, I would have a harder time actually counting the matches by counting lines. In the case of searching for the number of times a common word occurs in a longer text file, using the -c command line option is preferable.

source: https://docs.rackspace.com/docs/use-the-linux-grep-command
### `-r`: Recursive Search
#### Example 1: 
```
Caitlins-MBP:government caitimccallum$ grep -r 'California' Media/
Media//water_fees.txt:result, Chris Schneider, executive director of Central California
Media//Legal-aid_chief.txt:California.
Media//Unusual_Woodburn.txt:by California Rural Legal Assistance. Irma Luna, a community worker
Media//Unusual_Woodburn.txt:Studies in California show that most Mixtecs follow the tomato,
Media//Few_who_need.txt:California Bar Journal
Media//Few_who_need.txt:California lags far behind comparable states in funding legal
Media//Few_who_need.txt:the California Commission on Access to Justice, which also found
Media//Few_who_need.txt:California has the highest number of people in poverty in the
Media//Few_who_need.txt:poor jumped 30 percent, occurred in California, and nearly 25
Media//Few_who_need.txt:Even those with jobs are suffering: 26 percent of California
Media//Few_who_need.txt:Justice in California," examined how the legal needs of the state's
Media//Few_who_need.txt:California to meet the poor's legal needs, Connecticut and
Media//Few_who_need.txt:from two to 14 times more proportionately than California, despite
Media//Few_who_need.txt:the fact that California has the world's sixth largest economy.
Media//Few_who_need.txt:the legal needs of low-income Californians.
Media//Few_who_need.txt:every 10,000 poor Californians. Despite this bleak picture, the
Media//Few_who_need.txt:injustice," observed Justice Earl Johnson of the California Court
Media//Few_who_need.txt:denied," said Londen. "Clearly, California can - and must - do
Media//Nonprofit_Buys.txt:California Rural Legal Assistance has purchased an Oxnard
Media//Nonprofit_Buys.txt:signals California Rural Legal Assistance's intention to establish
Media//Nonprofit_Buys.txt:Latino to serve on the California Supreme Court.
Media//Nonprofit_Buys.txt:California Rural Legal Assistance has provided legal services to
Media//Nonprofit_Buys.txt:California Rural Legal Assistance operations.
Media//Legal_hotline.txt:California, was the only California application from 24 submitted
Media//Legal_hotline.txt:screw-up in Washington that California is losing having a program
Media//Legal_hotline.txt:Northern California.
Media//Legal_hotline.txt:Chisorom Okwuosa, legal services developer for the California
Media//Workers_aid_center.txt:California. It will provide brochures, form letters seeking back
Media//Working_for_Free.txt:The State Bar of California presented Zucker with its 2002
Media//Kiosks_for_court_forms.txt:A University of California, Irvine, study released Wednesday
Media//Kiosks_for_court_forms.txt:should clear the way for expansion throughout California. Locally,
Media//Kiosks_for_court_forms.txt:Bonnie Hough, supervising attorney for the California Judicial
Media//Coup_Reshapes_Legal_Aid.txt:multimillion-dollar grant from the California Endowment to fund a
Media//Lockyer_Warns.txt:State Atty. Gen. Bill Lockyer is warning Californians to beware
Media//Lockyer_Warns.txt:"The true nonprofit legal services organizations in California
Media//Lockyer_Warns.txt:The judge determined that Moore had violated California's Unfair
Media//Assuring_Underprivileged.txt:and the State Bar of California's Statewide Bench-Bar
Media//Assuring_Underprivileged.txt:services in the state of California is immeasurable," said Patricia
Media//Assuring_Underprivileged.txt:State Bar of California - have honored her.
Media//Free_Legal_Assistance.txt:California are using computerized video kiosks to prepare common
Media//Free_Legal_Assistance.txt:more Californians are going to court without a lawyer.
Media//Free_Legal_Assistance.txt:The State Bar of California has characterized the trend as "the
Media//Farm_workers.txt:In 1998, Cesar Chavez fasted for 36 days in California to
Media//Farm_workers.txt:that California farmworkers face greater risk of pesticide
Media//Farm_workers.txt:migrant farm workers in California, most of them Hispanic, have a
Media//Farm_workers.txt:with that from the California Cancer Registry.
Media//Understanding.txt:California to anchor the hotline.
Media//Bridging_legal_aid_gap.txt:Lash is associate dean at the University of Southern California
Media//Bridging_legal_aid_gap.txt:Law School. Johnson is a justice on California's Second District
Media//Bridging_legal_aid_gap.txt:Court of Appeal. Lash and Johnson are co-chairs of the California
Media//Bridging_legal_aid_gap.txt:In her year-long odyssey through the California justice system,
Media//Bridging_legal_aid_gap.txt:Access to Justice in California," prepared by the California
Media//Bridging_legal_aid_gap.txt:million poor Californians whose basic civil legal needs -- often
Media//Bridging_legal_aid_gap.txt:California has a critical dearth of legal services for the poor,
Media//Bridging_legal_aid_gap.txt:resources so that all Californians, regardless of income, have
Media//Bridging_legal_aid_gap.txt:California does have a strong network of legal aid organizations
Media//Bridging_legal_aid_gap.txt:all Californians. In 1999, thanks to Gov. Gray Davis and leaders in
Media//Bridging_legal_aid_gap.txt:aid for the poor. In addition, California Supreme Court Chief
Media//Bridging_legal_aid_gap.txt:state government support in California is at $84.5 million on legal
Media//Bridging_legal_aid_gap.txt:Californians spend on lawyers each year -- and that 2 percent would
Media//Bridging_legal_aid_gap.txt:or triples that of California. And democratic governments
Media//Bridging_legal_aid_gap.txt:world, California should certainly be able to adequately fund free
Media//Bridging_legal_aid_gap.txt:that the goal of equal access to justice for all Californians is
Media//Bridging_legal_aid_gap.txt:restraining order. California can -and must -- do better.
Caitlins-MBP:government caitimccallum$ grep -r 'California' Media/ | wc -l
      64
```
In this example, I'm able to use the grep command on a directory rather than a file thanks for the -r command line option. I think that if I were searching through a large file system such as docsearch, I might be interested in how many times my state, California, is mentioned within the /government directory. In this case I used a piping command with my grep command in order to see the actual number. I think this could be a very useful command for finding a keyword within a multitude of files without explicitly typing them out.

source: https://man7.org/linux/man-pages/man1/grep.1.html
#### Example 2: 
```
Caitlins-MBP:Alcohol_Problems caitimccallum$ grep -rci alcohol
./Session2-PDF.txt:142
./Session3-PDF.txt:199
./DraftRecom-PDF.txt:54
./Session4-PDF.txt:195
Caitlins-MBP:Alcohol_Problems caitimccallum$ 
```
In this example, I've used -r, and -c and -i all together in oder to list each file within the current working directory, which is docsearch/government/Alchohol_Problems, along with the count of matches to a case independent argument found within each file. I could see this being very useful for data analytics, expecially if I was searching for the frequency of a keyword between files and I'd like to perform arithmetic on the resulting count.

sources: https://man7.org/linux/man-pages/man1/grep.1.html, https://docs.rackspace.com/docs/use-the-linux-grep-command
### `-v`: Invert Match
#### Example 1:
```
Caitlins-MacBook-Pro:government caitimccallum$ grep -rc '§' | grep -v .txt:0
./About_LSC/commission_report.txt:55
./About_LSC/LegalServCorp_v_VelazquezDissent.txt:30
./About_LSC/LegalServCorp_v_VelazquezOpinion.txt:22
./About_LSC/Protocol_Regarding_Access.txt:1
./About_LSC/ODonnell_et_al_v_LSCdecision.txt:1
./About_LSC/State_Planning_Special_Report.txt:9
./Env_Prot_Agen/bill.txt:7
./Gen_Account_Office/og97032.txt:9
./Gen_Account_Office/og99036.txt:9
./Gen_Account_Office/og97019.txt:7
./Gen_Account_Office/og97020.txt:6
./Gen_Account_Office/ffm.txt:15
./Gen_Account_Office/og97023.txt:6
./Gen_Account_Office/og96011.txt:15
./Gen_Account_Office/Letter_Walkeraug17let.txt:11
./Gen_Account_Office/og97051.txt:8
./Gen_Account_Office/og97045.txt:8
./Gen_Account_Office/og97050.txt:11
./Gen_Account_Office/og96038.txt:8
./Gen_Account_Office/og98029.txt:7
./Gen_Account_Office/og96012.txt:13
./Gen_Account_Office/og97046.txt:7
./Gen_Account_Office/og97052.txt:11
./Gen_Account_Office/d03232sp.txt:11
./Gen_Account_Office/og97043.txt:6
./Gen_Account_Office/og96028.txt:11
./Gen_Account_Office/og96014.txt:8
./Gen_Account_Office/og97041.txt:12
./Gen_Account_Office/og96015.txt:8
./Gen_Account_Office/og96031.txt:11
./Gen_Account_Office/og96033.txt:7
./Gen_Account_Office/og96027.txt:6
./Gen_Account_Office/og98022.txt:8
./Gen_Account_Office/og96026.txt:11
./Gen_Account_Office/og96032.txt:7
./Gen_Account_Office/og96036.txt:12
./Gen_Account_Office/og96022.txt:12
./Gen_Account_Office/og96023.txt:7
./Gen_Account_Office/og96037.txt:9
./Gen_Account_Office/og98032.txt:6
./Gen_Account_Office/og98026.txt:7
./Gen_Account_Office/og98030.txt:8
./Gen_Account_Office/og98024.txt:9
./Gen_Account_Office/og96009.txt:9
./Gen_Account_Office/og96021.txt:7
./Gen_Account_Office/og98018.txt:7
./Gen_Account_Office/og96034.txt:8
./Gen_Account_Office/og98019.txt:7
./Gen_Account_Office/og96020.txt:9
./Gen_Account_Office/og96047.txt:8
./Gen_Account_Office/og98041.txt:8
./Gen_Account_Office/og97038.txt:7
./Gen_Account_Office/og97011.txt:13
./Gen_Account_Office/og97039.txt:9
./Gen_Account_Office/og98040.txt:8
./Gen_Account_Office/og96045.txt:8
./Gen_Account_Office/og98044.txt:10
./Gen_Account_Office/og96041.txt:22
./Gen_Account_Office/og97001.txt:9
./Gen_Account_Office/og97028.txt:12
./Gen_Account_Office/og96040.txt:9
./Gen_Account_Office/og98045.txt:8
./Gen_Account_Office/og96042.txt:8
./Gen_Account_Office/og97002.txt:9
./Gen_Account_Office/og97003.txt:7
./Gen_Account_Office/og96043.txt:12
./Gen_Account_Office/og98046.txt:7
./Post_Rate_Comm/Gleiman_gca2000.txt:1
./Post_Rate_Comm/ReportToCongress2002WEB.txt:22
Caitlins-MacBook-Pro:government caitimccallum$ 
```
In this example I've used two instances of the grep command. `grep -rc '§'` finds all instances of the character '§' in my current working directory, `

source: https://docs.rackspace.com/docs/use-the-linux-grep-command
#### Example 2: 
```

```

source:
### `-E`: Extended Regular Expressions
#### Example 1: 
```
Caitlins-MBP:Env_Prot_Agen caitimccallum$ grep -oE "[0-9]{4}" jeffordslieberm.txt 
2001
2001
2007
1997
1999
1990
2015
2015
2015
1990
2002
2006
2002
2007
2007
2015
2002
2015
2000
2000
2000
2001
2001
2002
2007
1997
1999
1990
2002
2001
2007
1997
1999
1990
2002
2007
1997
1999
1990
2002
2007
1997
1999
1990
2020
2001
2001
2007
2002
2007
2007
2002
2006
2004
2004
2001
2001
2001
1999
2015
2001
2001
2001
2000
2001
2001
2000
2020
2001
2001
2000
2000
2001
2001
1999
2010
2020
2000
2020
2020
1999
2010
2020
2020
2020
2007
2010
2010
2001
2007
2010
2010
2007
1999
2001
2020
2002
1999
2001
2002
2015
2002
2015
2002
1999
2010
2001
2015
1999
2001
2001
2001
1999
1970
2000
2015
2015
1999
1970
1980
1990
2000
2010
1980
1986
1993
2000
2001
2002
2002
2006
2007
2007
2007
2007
2015
2015
2015
2015
1999
2002
2007
2015
2015
1999
2005
2015
2015
2015
2015
2015
2010
2010
2015
2010
2010
1997
2001
2001
2002
2001
2000
2000
2000
1997
2001
2001
2000
2001
2001
2015
2007
2007
2015
2015
2015
2001
2001
2001
1179
1196
2001
1997
1997
2000
2000
2000
2000
1000
2000
1998
1998
2000
2000
2000
2001
2001
2001
2001
2001
1999
1999
2000
4402
2000
2001
2001
2001
2001
2001
2001
2001
2001
2001
2001
2001
1997
1997
1997
2000
2000
1992
2030
1992
2015
2030
1999
1999
2000
2000
1999
Caitlins-MBP:Env_Prot_Agen caitimccallum$
```
In this example, I'm using the -E command line option which allows for my PATTERN arguement "[0-9]{4}" to be used as an extended regular expression. Specifically, I am looking for a pattern of 4 characters, which can be from [0-9], this pattern is typically seen with a year such as '1999' or '2021' although it isn't always a year. In order to only print the matched parts of the matching line I used the -o command line option for readability. I could imagine that searching for the dates listed in a file would be a very handy. You could even use -r with the code given above to search recursively through a directory, though I did not for brevity.

Sources: https://man7.org/linux/man-pages/man1/grep.1.html, https://www.geeksforgeeks.org/grep-command-in-unixlinux/

#### Example 2:
```
Caitlins-MBP:Env_Prot_Agen caitimccallum$ grep -oE "[[:alpha:]]{2,10} [0-9]{2}, [0-9]{4}" jeffordslieberm.txt
October 31, 2001
May 17, 2001
May 17, 2001
May 17, 2001
October 18, 2001
Caitlins-MBP:Env_Prot_Agen caitimccallum$
```
Following from my first example using -E to implement extended regular expressions for pattern matching an expression within a file, I wanted to see if I could find all of the dates with the format "Month day, year". In order to accomplish this, I used three bracket expressions along with three ranges respective to them. The first "[[:alpha:]]{2,10}" indicates that the pattern of the first word should be 2-10 alphabetic characters, with the upper limit being set at the month with the longest name. The second peice, "[0-9]{2}" indicates that after a whitespace there should be a 2 digit number which can range from 00-99 inclusively. The third and final piece "[0-9]{4}" is the same arguement I used to find the occurences of 4 digit years in my last example, the only difference now is that it should be looking for that pattern to occur directly after both previous arguements and a ", ". Overall I think regEx is really interesting and useful so it's very valuable to be able to use regular expressions at the command line to search for specific patterns such as dates, special codes, ect.. 

Sources: https://man7.org/linux/man-pages/man1/grep.1.html, https://en.wikibooks.org/wiki/Regular_Expressions/POSIX-Extended_Regular_Expressions, https://www.gnu.org/software/findutils/manual/html_node/find_html/posix_002dextended-regular-expression-syntax.html
