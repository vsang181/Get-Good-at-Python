# Creating a Program Flowchart

To expand our organisation into a formation we can visualise, we will begin by creating a flowchart of how we expect our script to work. This will involve translating our previously written pseudocode into a graphical format.

Unlike writing pseudocode, creating a flowchart for a program may not always feel like a valuable investment of time. However, it can provide us with a clearer understanding of how the program should be structured and translated into the programming language we plan to use. In our case, we will be writing a Python script. Visualising the logical flow using distinct shapes for operations, decisions, and processes will become increasingly useful as we develop the script.

## Pseudocode Recap

Let us review our planned logic once again:

```
1. The script will make a request to a web page - supplied by the user.
2. The initial web page will be added to a dictionary with a value of 'yes'.
3. The web page will be parsed to search for any URLs starting with 'http'.
4. Each found URL will be stored in a list variable.
5. For each URL in the list:
    a. Check if the URL is already in the dictionary.
        i. If it is, skip it.
        ii. If it is not, check if it is within the allowed scope.
            - If it is within scope:
                * Add the URL to the dictionary with a value of 'yes'.
                * Request the page and repeat the parsing and storage process.
6. When no new URLs are left to process, print the list of all unique URLs found, one per line.
```
Flowchart Representation

Based on the pseudocode above, we have created a flowchart to visualise the program flow:

<img width="960" height="681" alt="image" src="https://github.com/user-attachments/assets/79473394-f29f-4769-b21a-741f887a2672" />

Flowchart Walkthrough

At the beginning of the flowchart, we added a clear starting point in the diagram.

1. Start
   
This represents the beginning of the script's execution.

3. Get URL from User
   
The user is prompted to supply a starting URL. This may be entered via terminal input or predefined in the code. The mechanism for this can be chosen during the scripting phase.

5. Add URL to Dictionary
   
The URL provided by the user is stored in a dictionary with the value 'yes', indicating it has already been visited.

7. Request Web Page

The script makes an HTTP request to the URL to retrieve the page contents.

9. Parse Page for URLs

The program scans the retrieved HTML to extract all links (URLs) starting with 'http'.

11. Loop Through Found URLs

Each extracted URL is then evaluated:

- Check if URL is Already in Dictionary
If the URL exists in the dictionary, it is skipped.

- If URL is New → Is it in Scope?
The program checks if the new URL falls within the allowed domain or boundary set by the user.

  - If Yes, it is added to the dictionary with 'yes' and the same process repeats for this new page (i.e., the script will request and parse the new URL).

  - If No, it is skipped.

7. All URLs Processed?

The loop continues until no more new URLs are left to process.

8. Print All Unique URLs

Finally, the script prints a list of all the unique URLs it discovered, one per line.

9. End

Marks the conclusion of the script's execution.
