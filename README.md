# Advanced Internet Applications – laboratory - ASP.NET Web Pages

**Description :** The aim of the exercice was to learn ASP.NET Web Pages technology, the Razor view engine and the basics of C# language by following a tutorial.
Because it was not obligatory, I didn't do the question n°7. Honnestly I am a not a big fan of this technology, and I prefered to spend more time on another project.  
In this description, I will describe the code and answer to all tutorial's questions.
**The code is located in WebApplication1 directory, not in packages directory**

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
In Asp.net, to see if a string is null or empty, we can use IsNullOrEmpty() function :
```
 if(!String.IsNullOrEmpty(Request["Name"]))//if the string isn't null or empty
        {
            //do something
        }
```

Such as it's explained in the exercise, the request variable stores the passed values regardless of the method ("get" or "post") they were sent by. To know which method is used, and execute appropriate instruction, we can use *IsPost* and *Request.HttpMethod* functions as following :
```
if (IsPost)//If it's a post method
{
    //do something
}
else if (Request.HttpMethod == "GET")//if it's a get method
{
    //do something
}
```
## Question 4
### Step 1 : Define and access to the list
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
To be able to display the strings of our session, we must define a naw variable and affect it the string list contained in session.
**Warning :** You must declare this variable as following, or it will also be considered as an object :
```
var Rules = Session["rules"] as List<string>;
```

### Step 2 ; The form
Here, we use the *IsPost* and *Request.HttpMethod* functions to determine which method is used. If it's a "post" method, we'll add the request variable in our Session["rules"] by using Add method, then do a redirect to our page. If it's a "get" method, we will first check if it's our first connection to the page by watching if Session["rules"] is defined. If it's defined, we do nothing and display the Session["rules"] content, else we define the Session["rules"] such as in step 1.
```
 if (IsPost)//if it's a post method
    {
        
        if (!String.IsNullOrEmpty(Request["Rule"]))//we check if the request variable isn't null
        {
            var Rules2 = Session["rules"] as List<string>;//to add an element to our session, we must declare a new variable, and affect it the Session["rules"] value (for the same reason that in step 1)
            Rules2.Add(Request["Rule"]);
            Session["rules"] = Rules2;
            Response.Redirect("Rules.cshtml");//we do a redirect
        }
    }
    else if (Request.HttpMethod == "GET")//if it's a get method
    {
        var Rules2 = Session["rules"] as List<string>;//If it's a get request, we check if the session is null (if it's the 1st connection, it will be null, else it's our redirection)
        if(Rules2 == null)
        {
            Session["rules"] = new List<string>()
            {
                "You fall, you lose",
                "The ring must be full of banana skin (if you slip you lose)",
                "There is only one round of 2 minutes",
                "If nobody fell after this delay, everybody lose, no winner",
                "Each loser must pay a beer to the ruler"
            };
        }

    }
    var Rules = Session["rules"] as List<string>;

}
```
## Question 5

In this question, I met a problem to load images and style sheet. To solve this problem, I replaced ~ by '..' (the '..'mean we go back to root project, I don't know for '~').
```
<link rel ="stylesheet" type="text/css" href="../Content/Style.css">
```

To define the title of the page (in the head), in the layout we set it to variable called "@Page.Title" :
```
 <head>
        <metacharset ="utf-8" />
        <title>@Page.Title</title>
        <link rel ="stylesheet" type="text/css" href="../Content/Style.css">
        <style>
       ...
 ```
And in the files Mark3.cshtml and Mark6.cshtml, we set this variable as following :
```
@{
    Page.Title = "Suit v6";
}
```

However, we're not forced to call this variable "Title", we can also call it "minou", it will also work (but not a good idea for maintenance).
In the layout file :
```
 <head>
        <metacharset ="utf-8" />
        <title>@Page.minou</title>
        <link rel ="stylesheet" type="text/css" href="../Content/Style.css">
        <style>
       ...
 ```
 In Mark6.cshtml :
 ```
@{
    Page.minou = "Suit v6";
}
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
For this question, I became the super vilain "lazyman", worse foe of all teachers. Seriously, I prefered to work on another project because it was not obligatory.

## Problems met
* See question 6 (to load image and style sheet)
* Visual Studio 2019 is slow. I spent more time to wait the app begin to run than code the app and write this desciption.
* I didn't really met problem for this exercice

## Conclusion
In this exercice, I learned the basics to do a project ASP.net technology, and saw his advantages. In my opinion, I find it's quite easy to handle this technology. Here, to access a variable or a function, you only need to type "@" before the variable's name, compared to php, where you need to write <"**php echo $variable ?>**", or javascript where you need to do an append.  
Well, in summary, it's very similar to the php frameworks, but I still prefered php frameworks. Maybe the goal of this assigment (and the next one) is to discover the advantages of a framework ?(with layout and MCV architecture). However, as I said before, the problem of ASP.net is you must work with visual studio, which is quite slow to run.   
But maybe I will change my mind in the next laboratory ? Who know? 
I thank my teacher, sir Piernik, for this exercice and new skills acquired.


