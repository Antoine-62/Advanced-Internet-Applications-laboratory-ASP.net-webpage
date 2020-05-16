# Advanced Internet Applications – laboratory - ASP.NET Web Pages

**Description :** The aim of the exercice was to learn ASP.NET Web Pages technology, the Razor view engine and the basics of C# language by following a tutorial.
Because it was not obligatory, I didn't do the question n°7, honnestly I am a not a big fan of this technology, and prefer to spend some time on the project.  
In this description, I will describe the code and answer to all tutorial's questions.

## Question 2

To access to the variable's value, we use "@" before the variable's name.
```
@{ 
    string name = "Robert  Paulson";
}
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
    <h1>Name</h1>
    <ul>
        @for (var i=0; i<10; i++)
        {
            <li>@name</li>
        }
    </ul>
</body>
</html>
```

## Question 3

## Question 4
### Step 1 : Define and access the list
First, we define a list of rules, and store it in our session.
```
 Session["rules"] = new List<string>()
            {
                "You fall, you lose",
                "The ring must be full of banana skin (if you slip you lose)",
                "There is only one round of 2 minutes",
                "If nobody fell after this delay, everybody lose, no winner",
                "Each loser must pay a beer to the ruler"
            };
```
You cannot access to the data of your session in the foreach, if you try, it will say it cannot works on object.  
To be able to display the strings in our session, we must define a variable and affect it the string list contained in session.
**Warning :** You must declare this variable as following, or it will also be considered as an object :
```
var Rules = Session["rules"] as List<string>;
```

### Step 2 ; The form
```
 var Rules = Session["rules"] as List<string>;
```
## Question 5

In this question, I met a problem to load images and style sheet. To solve this problem, I replaced ~ by '..' (the '..'mean we go back to root project, I don't know for '~').
```
<link rel ="stylesheet" type="text/css" href="../Content/Style.css">
```


When I try to display the _Layout.cshtml page, I have a 404 error.


## Question 6
We move the line of code responsible for setting the layout of the pages in *_PageStart.cshtml* :
```
@{
    Layout = "_Layout.cshtml";
}
```
When we run the app, everything works perfectly.


## Question 7
For this question, I become the super vilain "lazyman", worse foe of all teachers. Seriously, I prefered to work on other project because it was not obligatory.



