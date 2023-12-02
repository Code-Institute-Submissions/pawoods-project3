# CookBook

CookBook is a recipe sharing site designed for users to upload their own recipes and discover new and exciting dishes shared by other users. The site features a clean and simple interface, allowing a focus on the recipes rather than an accompanying post as you may find in a food blog.

With a user profile page also comes a way of storing, managing and easily accessing the user's own recipes, and quickly viewing those created by others that the user has liked, almost as a repository of recipes for future use.

The majority of data is displayed on the front-end as cards (recipes, categories, users) so as to give a consistent feel to the site no matter which page the user is viewing.

![Am I Responsive Screenshot](/static/images/readme/amiresponsive.webp)

[View Live Site Here](https://project-3-pawoods-dcf83ae94f0f.herokuapp.com/)

## Table of Contents

-   [UX](#ux)
    -   [User Stories](#user-stories)
    -   [Design](#design)
        -   [Wireframes](#wireframes)
        -   [Data Design](#data-design)
        -   [Visual Design](#visual-design)
            -   [Colours](#colours)
            -   [Fonts](#fonts)
            -   [Icons](#icons)
-   [Features](#features)
    -   [Current Features](#current-features)
        -   [Page Features Matrix](#page-features-matrix)
        -   [User Feature Permissions](#user-features-permissions)
    -   [Future Features](#future-features)
-   [Languages and Technologies](#languages-and-technologies)
-   [Testing](#testing)
    -   [Bugs](#bugs)
        -   [Fixed Bugs](#fixed-bugs)
        -   [Unfixed Bugs](#unfixed-bugs)
-   [Deployment](#deployment)
    -   [Live Deployment](#live-deployment)
    -   [Local Deployment](#local-deployment)
    -   [Requirements and env](#requirements-and-env)
    -   [MongoDB](#mongodb)
    -   [Heroku](#heroku)
-   [Credits](#credits)
    -   [Code Credits](#code-credits)
    -   [Support Credits](#support-credits)

## UX

### User stories

I wrote up the below user stories to ensure I kept the users in mind when creating the site. As I planned to have a multi level permission structure, I made a note to ensure each next level had full visibility and functionality of the user level below:

1. First time User - I should...

    - See a description of the site and be able to view all recipe and category content, including detailed recipes.
    - Have a clear navigation menu that is consistently accessible.
    - Have prompts to register for an account to get more from the site and find an easy to complete registration form with helpful form field feedback.
    - Find a contact page to submit feedback to admin with queries or comments.

2. Registered user (in addition to first time user) - I should...

    - Find a simple sign in page to log in to my account, giving feedback on incorrect account information.
    - See my details on a profile page, including personal information, recipes I have created and recipes I have liked.
    - Add new recipes with an entry form including dynamic fields for ingredients and instructions.
    - Update or delete my details, including recipes I have created.
    - Add/remove likes to recipes and view list of liked recipes on my profile page.

3. Super user (in addition to registered user) - I should...

    - Add new categories for use on recipes with a consistent submission form.
    - Update or delete category information on all categories and have changes show up across all existing applicable tags.
    - See a visual badge on my profile page to denote super user status.

4. Admin user (in addition to super user) - I should...
    - Have full access to update or delete recipes and categories directly from the cards.
    - See a page of all users with options to update details or delete users.
    - See dedicated buttons for changing the super user and admin status of all users.
    - See a page of messages sent through the contact page.
    - See a visual badge on my profile page to denote admin user status.

### Design

#### Wireframes

For all page wireframes, including mobile, tablet and desktop, please see [WIREFRAMES.md](WIREFRAMES.md) file.

#### Data design

As a data driven project, I wanted to make sure I thoroughly planned the data that would be stored in the database, how each document would link to eachother and how the user would interact with the data on the front end, considering full CRUD functionality. I Wrote up the following document plans to keep in mind when writing the python logic and applicable forms.

The project uses a non-relational database, meaning each collection is not directly related to one another as in a relational database. This meant that where a document on one collection needed to reference one in another, I had to ensure the correct data type and structure to allow this. 

Users:

```
{
    _id: ObjectId,
    user_id: integer,
    f_name: string,
    l_name: string,
    username: string,
    email: string,
    password: hashed password,
    user_since: datetime object,
    photo_url: string,
    is_super: boolean,
    is_admin: boolean
}
```

Categories:

```
{
    _id: ObjectId,
    category_name: string,
    category_description: string,
    category_color: string
}
```

Recipes:

```
{
    _id: ObjectId
    recipe_name: string,
    recipe_description: string,
    categories: [ //multiple categories can be added
        {
            _id: (from category)
            category_name: (from category),
            category_description: (from category),
            category_color: (from category)
        }
    ],
    ingredients: [
        "Ingredient 1", "Ingredient 2" ...
    ],
    "Instructions": [
        "Instruction 1", "Instruction 2" ...
    ],
    "prep_time": integer,
    "cook _time": integer,
    "serves": Integer,
    "likes": {
        count: integer,
        id: [
            (id from user), (id from user2)...
        ]
    },
    "created_by": {
        "username": (from user),
        "user_id": (from user)
    },
    "created_date": datetime object
}
```

Messages:

```
{
    _id: ObjectId,
    user_name: string (from user if signed in),
    user_email: string (from user if signed in),
    message_date: datetime object,
    message_content: string
}
```

#### Visual Design

##### Colours

I used [coolors](https://coolors.co/) to design my colour palette, I wanted to keep the majority of the site light in colour to give a clean and simple look while using some darker accent colours on the header, footer, menu and buttons. This was the palette I settled on as it gave a good contrast between the light and dark colours while not being visually overwhelming for the user.

![Coolors Screenshot](/static/images/readme/coolors.webp)

##### Fonts

I used [Google Fonts](https://fonts.google.com/) for the fonts on the site, choosing to user one font for the logo and page/section headers and another for the majority of the text on the site. Using sample text for the site, I settled on "Courgette" for the logo and header font and "Nunito" for the main body text as these fonts work well together, provide good readability for the site users with the accent text giving an extra flourish to the headers.

Courgette

![Courgette Font Screenshot](/static/images/readme/courgette.webp)

Nunito

![Nunito Font Screenshot](/static/images/readme/nunito.webp)

##### Icons

I used a mixture of icon sources on the site, initially using the built in Google Icons bundled with Materialize. As I got further into the project, i realised i needed more icon choice for the menu element of the site, so I chose to add Font Awesome to the project to make use of the wider range of icons available here. Below is a graphic representation of the icons used on different parts of the site.

![Icons Screenshot](/static/images/readme/icons.webp)

I also added a favicon to the project using [Favicon](https://favicon.io/). I replicated the main dark green colour of the site as the background colour with white text and rounded edges to match the card elements on the site.

![Favicon Screenshot](/static/images/readme/favicon.webp)

## Features

### Current Features

To keep aligned with the user stories, an extensive list of features for the site was compiled and prioritised to meet all the points of each user. Below is a list of each feature included, with site locations. Features not included but considered are contained in the [Future Features](#future-features) section.

<details>
<summary>Recipe Cards</summary>

-   Found on home, recipes, _filtered_ recipes and profile pages. Has backup image if users doesn't input one on create.

![Recipe Card Screenshot](/static/images/readme/features/recipecard.webp)

- More information revealed by clicking on more (three vertical dots) icon.

![Recipe Card Screenshot 2](/static/images/readme/features/recipecard2.webp)

</details>
<details>
<summary>Category Cards</summary>

-   Found on categories page.

![Category Card Screenshot](/static/images/readme/features/categorycard.webp)

</details>
<details>
<summary>User Cards</summary>

-   Found on the users page. Has backup blank user image if no photo on account.

![User Card Screenshot](/static/images/readme/features/usercard.webp)

- More information revealed by clicking on more (three vertical dots) icon.

![User Card Screenshot 2](/static/images/readme/features/usercard2.webp)

</details>
<details>
<summary>Profile Card</summary>

-   Full card found on the individual users profile. Reduced info found at top of menu element when signed in. Has backup blank user image if user hasn't added photo.

![Profile Card Screenshot](/static/images/readme/features/profilecard.webp)

![Profile Card Screenshot2](/static/images/readme/features/profilecard2.webp)

</details>
<details>
<summary>Slide-out Menu</summary>

-   Found on every page by clicking the lines in the top right of the header element.

Signed in

![Menu Signed In Screenshot](/static/images/readme/features/menusignedin.webp)

Signed out

![Menu Signed Out Screenshot](/static/images/readme/features/menusignedout.webp)

</details>
<details>
<summary>Flashed Messages Banner</summary>

-   Found underneath page header when user completes action that triggers feedback.

![Flash Banner Screenshot](/static/images/readme/features/flashbanner.webp)

</details>

<details>
<summary>Register CTA Button</summary>

-   Found on the home page at the end of the "About" section. Link also found on the slide out menu and sign in pages.

![Register CTA Button Screenshot](/static/images/readme/features/registercta.webp)

![Register Menu Link Screenshot](/static/images/readme/features/menusignedout.webp)

</details>
<details>
<summary>Likes Button with Counter</summary>

-   Found on all recipe cards. Button without counter can also be found on the "More" button on each recipe details page if signed in.

Liked

![Liked Button Screenshot](/static/images/readme/features/liked.webp)

Unliked

![Unliked Button Screenshot](/static/images/readme/features/unliked.webp)

</details>
<details>
<summary>Pop Out Button</summary>

-   Found on all recipe cards.

![Pop Out Button Screenshot](/static/images/readme/features/popout.webp)

</details>
<details>
<summary>Edit Button</summary>

-   Found on all recipe cards if user is the recipe owner or admin. Found on all full category cards if the user is super user or admin. Found on all user profiles and user cards.

![Edit Button Screenshot](/static/images/readme/features/editbutton.webp)

</details>
<details>
<summary>Delete Button</summary>

-   Found on all recipe cards if user is the recipe owner or admin. Found on all full category cards if the user is super user or admin. Found on all user profiles and user cards.

![Delete Button Screenshot](/static/images/readme/features/deletebutton.webp)

</details>
<details>
<summary>Floating Action Button</summary>

-   Found on recipes, _filtered_ recipes, recipe details and categories pages.

Add New 

![Add Action Button Screenshot](/static/images/readme/features/addaction.webp)

More

![More Action Button Screenshot](/static/images/readme/features/moreaction.webp)

</details>
<details>
<summary>Recipe Filter Button</summary>

-   Found on all category cards, in the reveal section of recipe cards and in the "Categories" section of the recipe details accrodion.

Category Card

![Filter Button Screenshot](/static/images/readme/features/filterbutton.webp)

Recipe Card

![Filter Buttons Screenshot](/static/images/readme/features/filterbuttons.webp)

</details>
<details>
<summary>Password Visibility Button</summary>

-   Found at the end of all password input elements; Register, sign in, edit details and in the confirmation modal when editing or deleting users.

![Password Visibility Button Screenshot](/static/images/readme/features/passwordvisibility.webp)

</details>
<details>
<summary>Password Confirmation Modal</summary>

-   Found when attempting to update user details or delete profile.

![Password Confirmation Modal Screenshot](/static/images/readme/features/passwordcheck.webp)

</details>
<details>
<summary>Defensive Modal</summary>

-   Found when attempting to complete any destructive action, delete recipe, category or account or sign out.

![Defensive Modal Screenshot](/static/images/readme/features/defensivemodal.webp)

![Defensive Modal Screenshot 2](/static/images/readme/features/defensivemodal2.webp)

</details>
<details>
<summary>Recipe Details Accordion</summary>

-   Found on recipe details page, containing ingredients, instructions, description and categories.

Closed

![Recipe Accordion Closed Screenshot](/static/images/readme/features/recipeaccordionclosed.webp)

Open

![Recipe Accordion Open Screenshot](/static/images/readme/features/recipeaccordionopen.webp)

</details>
<details>
<summary>Messages Accordion</summary>

-   Found on messages page, containing header info of user and time and message content in the body.

![Messages Accordion Screenshot](/static/images/readme/features/messagesaccordion.webp)

</details>
<details>
<summary>Dynamic Ingredients/Instructions Form Fields</summary>

-   Found on add and edit recipe pages, adds input after current with ➕ icon and removes current with ➖ icon. Javascript code written to add one input if all in that section are deleted.

![Input Fields Screenshot](/static/images/readme/features/inputfields.webp)

</details>

#### User Feature Permissions

To help guide me within the development process and ensure I made all features available for the relevent users, I found it helpful to visualise applicable users for each feature in a table:

| PAGE/Feature             | Anonymous User | Registered User | Super User | Admin |
| :----------------------- | :------------: | :-------------: | :--------: | :---: |
| HOME                     |       ✅       |       ✅        |     ✅     |  ✅   |
| New Recipes              |       ✅       |       ✅        |     ✅     |  ✅   |
| Popular Recipes          |       ✅       |       ✅        |     ✅     |  ✅   |
| RECIPES/FILTERED RECIPES |       ✅       |       ✅        |     ✅     |  ✅   |
| Recipe Card              |       ✅       |       ✅        |     ✅     |  ✅   |
| - Likes                  |      View      |       ✅        |     ✅     |  ✅   |
| - Details                |       ✅       |       ✅        |     ✅     |  ✅   |
| - Edit                   |       ❌       |    If Owner     |  If Owner  |  ✅   |
| - Delete                 |       ❌       |    If Owner     |  If Owner  |  ✅   |
| - Category Filters       |       ✅       |       ✅        |     ✅     |  ✅   |
| Menu (Signed Out)        |       ✅       |       ✅        |     ✅     |  ✅   |
| - Home                   |       ✅       |       ✅        |     ✅     |  ✅   |
| - Recipes                |       ✅       |       ✅        |     ✅     |  ✅   |
| - Sign In                |       ✅       |       ✅        |     ✅     |  ✅   |
| - Register               |       ✅       |       ✅        |     ✅     |  ✅   |
| - Contact                |       ✅       |       ✅        |     ✅     |  ✅   |
| Menu (Signed In)         |       ❌       |       ✅        |     ✅     |  ✅   |
| - Home                   |       ❌       |       ✅        |     ✅     |  ✅   |
| - Recipes                |       ❌       |       ✅        |     ✅     |  ✅   |
| - Add Recipe             |       ❌       |       ✅        |     ✅     |  ✅   |
| - Categories             |       ❌       |       ✅        |     ✅     |  ✅   |
| - Add Categories         |       ❌       |       ❌        |     ✅     |  ✅   |
| - Profile                |       ❌       |       ✅        |     ✅     |  ✅   |
| - Contact                |       ❌       |       ✅        |     ✅     |  ✅   |
| - Users                  |       ❌       |       ❌        |     ❌     |  ✅   |
| - Messages               |       ❌       |       ❌        |     ❌     |  ✅   |
| - Sign Out               |       ❌       |       ✅        |     ✅     |  ✅   |
| ADD RECIPE               |       ❌       |       ✅        |     ✅     |  ✅   |
| EDIT RECIPE              |       ❌       |    If Owner     |  If Owner  |  ✅   |
| CONTACT                  |       ✅       |       ✅        |     ✅     |  ✅   |
| Contact Form             |       ✅       |       ✅        |     ✅     |  ✅   |
| - Pre Populated          |       ❌       |       ✅        |     ✅     |  ✅   |
| CATEGORIES               |       ✅       |       ✅        |     ✅     |  ✅   |
| Category Card            |       ✅       |       ✅        |     ✅     |  ✅   |
| - Filter Button          |       ✅       |       ✅        |     ✅     |  ✅   |
| - Edit                   |       ❌       |       ❌        |     ✅     |  ✅   |
| - Delete                 |       ❌       |       ❌        |     ✅     |  ✅   |
| ADD CATEGORY             |       ❌       |       ❌        |     ✅     |  ✅   |
| EDIT CATEGORY            |       ❌       |       ❌        |     ✅     |  ✅   |
| PROFILE (User Specific)  |       ❌       |       ✅        |     ✅     |  ✅   |
| Liked Recipe Cards       |       ❌       |       ✅        |     ✅     |  ✅   |
| Owned Recipe Cards       |       ❌       |       ✅        |     ✅     |  ✅   |
| Delete Account           |       ❌       |       ✅        |     ✅     |  ✅   |
| EDIT DETAILS             |       ❌       |     If User     |  If User   |  ✅   |
| USERS                    |       ❌       |       ❌        |     ❌     |  ✅   |
| User Card                |       ❌       |       ❌        |     ❌     |  ✅   |
| Make Super               |       ❌       |       ❌        |     ❌     |  ✅   |
| Make Admin               |       ❌       |       ❌        |     ❌     |  ✅   |
| Edit Details             |       ❌       |       ❌        |     ❌     |  ✅   |
| Delete Account           |       ❌       |       ❌        |     ❌     |  ✅   |
| RECIPE DETAILS           |       ✅       |       ✅        |     ✅     |  ✅   |
| All Details              |       ✅       |       ✅        |     ✅     |  ✅   |
| Likes                    |      View      |       ✅        |     ✅     |  ✅   |
| Edit                     |       ❌       |    If Owner     |  If Owner  |  ✅   |
| Delete                   |       ❌       |    If Owner     |  If Owner  |  ✅   |

### Future Features

Features that were part of my initial scope but deemed a lower priority and therefore forming my future features are as follows:

-   Direct photo upload from user, using cloudinary or similar technology - As noted in testing, the URL links add the risk of large files and therefore long page loads and lower performance.

-   Add shopping list feature to user profile where users can click an icon next to ingredients on a recipe to add to a shopping list for future use.

-   Add function to recipe details page that stops the screen going to sleep so users can follow along with the recipe whilst cooking, without having to touch the screen to wake it.

## Languages and Technologies

The below table shows the technologies and languages used in this project and their use or location across the site/project.

| Language/Technology | Use/location in Project                                                                                                                                                                                                                |
| :------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HTML                | Used to build templates for all pages on site                                                                                                                                                                                          |
| CSS                 | Used to customise materialize styling on all elements                                                                                                                                                                                  |
| JavaScript          | Used to initialize Materialize elements, add and remove buttons for recipe instructions and ingedients and to remove the flashed messages element                                                                                      |
| Python              | Used for majority of logic on site, processing data between database and front end                                                                                                                                                     |
| MongoDB             | Storing data entered by users                                                                                                                                                                                                          |
| Flask               | Used within app.py file with app.routes housing majority of python logic                                                                                                                                                               |
| Jinja               | Used to template front end sites, using loops over lists and if statements to check user status                                                                                                                                        |
| Werkzeug            | Used during development process to debug when issues were present                                                                                                                                                                      |
| Codeanywhere        | Used as the main dev environment in the first half of the project                                                                                                                                                                      |
| Visual Studio Code  | Used as the main dev environment in the second half of the project (codeanywhere down)                                                                                                                                                 |
| Git        | Used for version control within development environment                                                                                                                                                                      |
| GitHub        | Used to store project repo                                                                                                                                                                      |
| Datetime            | Imported to get datetime objects for users registry dates and recipe and message creation dates                                                                                                                                        |
| Heroku              | Used to deploy the live site                                                                                                                                                                                                           |
| Materialize         | Used for many individual elements; menu, accordion, cards, reveal elements, modals, tooltipped elements and action buttons. Also used for basic styling with helper classes for colour, button size, element positioning and size etc. |
| Google Fonts        | Used for site fonts; Courgette and Nunito                                                                                                                                                                                              |
| Google Icons        | Used for icons across site, primarily forms and cards                                                                                                                                                                                  |
| Font Awesome        | Used for icons within the menu element                                                                                                                                                                                                 |
| Favicon             | Used for site favicon                                                                                                                                                                                                                  |
|Code Institute Python Linter | Used to test the app.py file for Pep8 compliance |

## Testing

☑️☑️☑️☑️☑️

For all manual user testing, lighthouse performance testing and code validation, please see [TESTING.md](TESTING.md) file.

☑️☑️☑️☑️☑️

### Bugs

During the development process, I used Google Chrome Devtools to manually test the features myself as I added them, following the user stories as I built the site and keeping a list of the bugs and their fixes along the way.

#### Fixed bugs

1. Issue where user id's were not incrementing as expected.

    - Fixed by changing key in IF statement from "user" to "user_id"

2. Issue with key errors displaying when singing out and being redirected to home screen.

    - Fixed by changing the session check syntax from session["user"] to "user" in session.

3. Bug noted where dynamically adding fields in form and submitting empty would result in pushing empty strings into the array.

    - Fixed by filtering out the empty strings from the list before buidling the dictionary in the funtion.

4. Bug using accordion and expandable collapsibles where jQuery .collapsible() overwrote the .expandable JavaScript.

    - Fixed by adding a second class (messages) to the accordion element and the jQuery selector.

5. Bug found where admin cannot see edit and delete buttons on other users recipe cards on home screen under popular recipes.

    - fixed by adding in the missing or user.is_admin to the jinja if statement.

6. Bug found where users could edit or delete other users recipes from the liked recipe section of their profile page.

    - Fixed by adding in the missing jinja if statement around the edit and delete buttons.

7. Bug found where bringing up the delete user modal from the user page caused the input to be unclickable.

    - Fixed by changing the id and name of the input by appending the user id to the end of the string meaning they would each now be unique.

8. Bug created by the above fix meant users deleting their account from their profile faced a Werkzeug error.

    - Fixed by adding the user's id to the id of the input field so it can be picked up in the same way as from the users page by the app.route function.

9. Bug found where custom user ids were being reused when a user deleted their account, leading to the likes from the previous user showing up for the next user to register.

    - Fixed by creating a new DB collection with a single document called used_ids. On every register, the generated id is pushed into an array on this document and this is what is checked instead of the user_id from the users DB collection.

10. Bug found where dynamic "instruction" or "ingredients" fields could all be removed from the add_recipe form.
    - Fixed by adding in a check on remove() function to count the children of the list and add another child if all input field children are deleted.

#### Unfixed Bugs

1. Redirect using the session url works well in majority of normal use cases, although where a user navigates using back button, the browser will load a cahced version of the page and won't overwrite the url in session. Meaning, when a user then triggers another function (like, delete etc.), they will be returned to the last page that stores the url in session.

## Deployment

### Live

The site was deployed to [Heroku](https://www.heroku.com/platform). View the live site [here!](https://project-3-pawoods-dcf83ae94f0f.herokuapp.com/)

### Local

To access this [GitHub Repository](https://github.com/pawoods/project2) locally, you can follow the below guides to either clone or fork the repo.

#### Cloning

Cloning this repository will pull down a full copy to a local computer or remote virtual machine within a codespace. You can then `push` or `pull` your own or other users changes to the original repo. To clone this repo, follow the below step by step instructions:

1. Navigate to the [GitHub Repository](https://github.com/pawoods/project3) for this project.
2. Click the `<> Code` button above the list of files.
3. Chose whether to clone using HTTPS, SSH, or GitHub CLI and copy the URL.
4. Open Git Bash or Terminal.
5. Change the current working directory to the location where you want the cloned repo.
6. Use the `git clone` command followed by the copied URL.
   ```
   git clone https://github.com/pawoods/project3.git
   ```
7. Press enter to create your local clone.

#### Forking

Forking this repository will create a parallel version in your own GitHub account, allowing changes to be made with no change to the original repo. To fork this repo, follow the below step by step instructions:

1. Navigate to the [GitHub Repository](https://github.com/pawoods/project2) for this project.
2. Click `Fork` button in top right under main navigation bar.
3. A copy of this repo should now exist in your GitHub account.

#### Requirements and env

After cloning or forking the repo, the dependancies within the requirements.txt need to be installed using the command `pip3 install -r requirements.txt`

Any other packages installed in the project after cloning or forking the repo can be added to the requirements.txt file by using the command `pip3 freeze --local > requirements.txt`

An `env.py` file will also need to be created at root-level to contain environment variables that should not be pushed to GitHub, the `env.py` file is listed in the `.gitignore` file to ensure this.

The local `env.py` file will look something like below but with values unique to the user where indicated, these will be covered in the [MongoDB](#mongodb) section.

```
import os

os.environ.setdefault("IP", "0.0.0.0")
os.environ.setdefault("PORT", "5000")
os.environ.setdefault("SECRET_KEY", "any string value")
os.environ.setdefault("MONGO_DBNAME", "name of user's mongoDB database")
os.environ.setdefault("MONGO_URI", "user's mongoDB connection string")
```

#### MongoDB

The project uses [MongoDB](https://www.mongodb.com/cloud/atlas/register?utm_content=rlsapostreg&utm_source=google&utm_campaign=search_gs_pl_evergreen_atlas_general_retarget-brand-postreg_gic-null_emea-all_ps-all_desktop_eng_lead&utm_term=&utm_medium=cpc_paid_search&utm_ad=&utm_ad_campaign_id=14412646473&adgroup=131761130372&cq_cmp=14412646473&gad_source=1&gclid=CjwKCAiA9ourBhAVEiwA3L5RFqrqGrd12Y8t-DXSb2zA7gWH0_9lTYiylpHAfvjeRKf9R8fJvlMgHhoCrt8QAvD_BwE) non relational database. To connect your repo up to your own database, these are the steps to follow:

1. Sign up for an account with MongoDB.
2. Select a tier, cloud provider and locality (As I am in the UK, I selected Ireland)
3. Select a Cluster Name or Leave default Cluster0 and click create.
4. Navigate to Database Access and set up a new database user. 
5. Select Password as the authentication method and input a username and password, these will be used in the connection string within the env.py file. Only use letters and numbers to avoid connection issues.
6. Select a built in role of read and write to any database.
7. Click Create. 
8. Navigate to Network Access and click Add IP Address.
9. Select whether to add a local IP address or to allow access from anywhere.
10. Confirm.
11. Navigate to Database and click on Browse Collections next to the name of the Cluster set up in step 3.
12. Click Add My Own Data and add a database name and collection name. This database name should be added to the env.py file as the value for "MONGO_DBNAME".
13. Click the plus sign next to the database name to add further collections - You will need a total of four collections within the database: users, recipes, categories and messages. Any different names would need to then be updated everywhere the collections are called in the app.py file.
14. From the Overview tab in the Cluster, click the Connect button. 
15. Follow the connection instructions for your preferred connection method (I chose to connect using the Python Driver)
16. Copy the connection string to the env.py file as the value for "MONGO_URI".

- NOTE: You will need to replace the ``<password>`` placeholder with the user password created in step 5.
- NOTE: I experienced issues when connecting with the above method and found I had to add the database name created in step 12 to the connection string between the / and ? - after this, I experienced no further connection issues.

#### Heroku

To deploy your app on [Heroku](https://www.heroku.com/platform), these are the steps to follow: 

1. Sign up for an account with Heroku.
2. Click New button and select Create New App.
3. Choose a name for your app. This must be unique.
4. Select a region and click Create App.
5. Choose your connection method, I used automatic deployment from GitHub repo. 
6. Make sure your GitHub profile is displayed and search for the repository. You may need to connect to your GitHub account if not completed at registration.
7. Once the repo is found, click connect.
8. Navigate to Settings tab and click on Reveal Config Vars
9. Each variable from the env.py file will need to be replicated here in key value pairs and without quotes e.g. key = ``PORT`` and value = ``5000``
10. Once all config vars are added, you can now navigate back to the deploy tab and click Enable Automatic Deploys, select the branch to deploy and click Deploy.
11. Once complete, you can click Open App to view the live site.
- NOTE: The live site will now update any time changes are pushed to the connected GitHub repository.

## Credits

### Code Credits

$ne operator - [Developers Log Blog](https://developerslogblog.wordpress.com/2019/10/15/mongodb-how-to-filter-by-multiple-fields/)

Recipe card backup image of a set dinner table - [The Plainsman Museum](https://www.plainsmanmuseum.org/single-post/formal-table-setting)

User backup profile image - [Pixabay](https://pixabay.com/vectors/blank-profile-picture-mystery-man-973460/)

### Support Credits

A big thank you to my mentor Martina Terlevic and cohort facilitators Iris Smok and Irene Neville for their help and encouragement with the project.

Another big thank you goes out to my Code Institute cohort team and the wider Code Institute community on Slack for providing help, testing and encouragement when needed.
