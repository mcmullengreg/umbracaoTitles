#Umbraco Title Tags

This code is a cleaned up version of a previously posted git. It uses the level of a node to define the loop 

process.

##Assumptions
1. You are using razor to build macros
2. You have document type variables named shortPageTitle and pageTitle
    + These can be modified or removed in the code as needed

This code is provided as is with no support. 

##Code Breakdown

Define variables, clear `var current`

    var pageLevel = @Model.Level;
    var current = ""; 

Run the loop based off of the page level, descending to add on to the `pageLevel`.

    for (var i = pageLevel; i >= 1; i--){
    
    }

Within the loop, define your divider. Use `" | "` if `i==2` else if `i > 2` use `" - "` else do nothing

    var divider = (i == 2) ? " | " : 
                  (i > 2) ? " - " : "";

Using `current+=` run through the loop, adding a page title and divider. Utilizing the `shortPageTitle` or 

`pageTitle` before the fallback of `name`

    current += (Model.AncestorOrSelf(i).HasValue("shortPageTitle") && pageLevel != 1) ?
                Model.AncestorOrSelf(i).shortPageTitle + divider : 
               (Model.AncestorOrSelf(i).HasValue("pageTitle")) ? 
                Model.AncestorOrSelf(i).pageTitle + divider :
                Model.AncestorOrSelf(i).Name + divider;

Output the page title to your screen

    @current

##Adjustments
Adjust as you see fit to meet your needs.
