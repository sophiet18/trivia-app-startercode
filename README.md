# lesson 3 

in short, this has been the most fun and yet frustrating day since starting this course. 

On the one hand, I enjoyed very much the thrill of working on a project that would deliver an actual app but on the other hand, every time I ran the app I got a heart attack ð

I had the audacity and patience to read through every error message, look up and experiemnt with solutions from stackoverflow and eventually finish till I couldn't go any further cause android studio was throwing me gradle errors.... 

someday I'll come back to this and sort it out ð

# Fragment

each destination screen is built using FRAGMENT - a UI component 

each activity can contain one or more fragments and they could be swapped for other fragments 

primarily exists to support more dynamic and flexible UI designs on large screens

activity operates as a frame that contains UI fragments and can provide elements that support it 

operates like view in layout BUT must create a subclass of fragment to actually use it 

screens are stacked together and controlled by the fragment stack manager 

# ACTIVITY VS FRAGMENT 

ACTIVITY
â¢ call setContentView in onCreate to tell android which activity to use the activity then inflates the layout and places it correctly within the activity's layout hierarchy
â¢ activities inherit from the context class 

FRAGMENT 
â¢ manually inflate and return the inflated layout within the onCreateView method 
â¢  independent of onCreate 
â¢ do not inherit from context class, so need to use the context property within a fragment to access app data associated with the context - like string and image resources 

ð onCreateView()
â¢ used to inflate the view instead of onCreate like in an activity 

ð context
â¢ this is the property from within a fragment used to gain access to image resources and strings

ð Activity layout 
â¢ UI fragments that contain a layout and occupy space within 

#Navigation
ð¡ when trying this out on your own, make sure the dependencies are in place!!! 

1ï¸â£add navigation graph resource

2ï¸â£ add NavHostFragment 
â¢ acts as a host for each fragment in the activity navigation graph as users move between pages, it automatically manages the stack 

3ï¸â£ add fragments to the navigation graph

4ï¸â£ connect fragments in the graph with actions
â¢ adding and connecting screens don't actually do anything, they simply represent POSSIBLE pathways from one to fragment to another 

5ï¸â£ create onClickListener
ð¡the method they suggested in the course did not work!! 

6ï¸â£  find Navigation controller
â¢ this is A CLASS used to manage navigation with our nav host fragment 
â¢ the navigation host fragment is the parent in the view hierarchy of our current fragment aka the title screen fragment 
â¢ which means that we can travel up the hierarchy and find it (title screen) from any view in our fragment even the play button! 

7ï¸â£  navigate with action 
PopTo NOT INCLUSIVE
â¢ pops off everything on the back stack until it finds the referenced fragment transaction
PopTo Inclusive
â¢ pops off everything on the back stack, including the referenced fragment transaction 

8ï¸â£  control animation with navigation listeners 
â¢ to control where and when the drawer menu appears when 
â¢ set inside onCreate() by calling it whenever the destination changes - when the id of our NavDestination matches the start destination of our graph, weâll unlock the drawerLayout; otherwise, weâll lock and close the drawerLayout.

# NAVIGATION METHODS & FUNCTIONALITY 

ð APP DRAWER NAVIGATION
â¢ defaults to poping everything off the backstack except for the start destination 

ð MENU NAVIGATION
â¢ adds to the backstack from the current position

ð  DRAWER LAYOUT
â¢ provides the foundation for the sliding behaviour of the navigation drawer

ð  NAVIGATION VIEW
â¢ material design container that provides the look, feel, and functionality of the navigation drawer 

# Intent

INTENTS - are descriptions that the system uses to locate activities on behalf of applications 

ðEXPLICIT INTENT
â¢ launches specific activity using the name of the target activity class  
â¢ typically used only to launch other activities WITHIN the application 
â¢ happens when you navigate to other activities in the navigation graph 

ð IMPLICIT INTENT 
â¢ provides an abstract description of the operation to be performed 
â¢ most often used to launch activities that are exposed by other applications
â¢ the system may not have any apps that can handle an implicit intent
â¢ when multiple android apps can handle the same implicit intent - android will provide a pop-up list of compatible apps to let the user select the desired one to handle the request 

ðimportance: allows an app to request something from another app without having to know anything about that other app - when text is shared from our app with implicit intent - the app does not need to know the channel it is shared, just needs to know that there are applications/channels that can handle the "text-sharing" request

ð  INTENT ACTIONS 
â¢ actions in each implicit intent and are DIFFERENT from those in the navigation graph 
â¢ used here to describe the type of thing that is to be done 
â¢ COMMON EXAMPLES = view(action_view), dial(action_dial), or edit(action_edit)

ð INTENT CATEGORIES 
â¢ adds a subtype to the intent-action to disambiguate the action
â¢  but aren't always used 
â¢ EXAMPLE = the categories used along with the main entry point to launch available music players, mapping applications ... etc

ð  INTENT DATA TYPE (MIME DATA TYPE)
â¢ implicit intents can include a data type like text or jpeg image which allows applications to be chosen based on what data type can be accepted
â¢ EXAMPLE = sender intent  

ð  INTENT EXTRA
â¢ used to provide arguments for the intent 
â¢ some argument types have predefined keys like text 

â ï¸  ALL ACTIVITIES MUST BE REGISTERED IN THE ANDROID MANIFEST TO BE LAUNCHED 
â¢ explicit activities can be launched with a <activity> tag
â¢ implicit activities require a <intent-filter> tag - it is used to expose that your activity can respond to an implicit intent with a certain action, category or type 
â¢ if a given activity in the app doesn't have this <intent-filter> it will not launch in the app 
