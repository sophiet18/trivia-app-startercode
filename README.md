#lesson 3 
in short, this has been the most fun and yet frustrating day since starting this course. 

On the one hand, I enjoyed very much the thrill of working on a project that would deliver an actual app but on the other hand, every time I ran the app I got a heart attack 😔

I had the audacity and patience to read through every error message, look up and experiemnt with solutions from stackoverflow and eventually finish till I couldn't go any further cause android studio was throwing me gradle errors.... 

someday I'll come back to this and sort it out 🌚

#Fragments
each destination screen is built using FRAGMENT - a UI component 

each activity can contain one or more fragments and they could be swapped for other fragments 

primarily exists to support more dynamic and flexible UI designs on large screens

activity operates as a frame that contains UI fragments and can provide elements that support it 

operates like view in layout BUT must create a subclass of fragment to actually use it 

screens are stacked together and controlled by the fragment stack manager 

ACTIVITY VS FRAGMENT 

ACTIVITY
• call setContentView in onCreate to tell android which activity to use the activity then inflates the layout and places it correctly within the activity's layout hierarchy
• activities inherit from the context class 

FRAGMENT 
• manually inflate and return the inflated layout within the onCreateView method 
•  independent of onCreate 
• do not inherit from context class, so need to use the context property within a fragment to access app data associated with the context - like string and image resources 

📌 onCreateView()
• used to inflate the view instead of onCreate like in an activity 

📌 context
• this is the property from within a fragment used to gain access to image resources and strings

📌 Activity layout 
• UI fragments that contain a layout and occupy space within 

#Navigation
💡 when trying this out on your own, make sure the dependencies are in place!!! 

1️⃣add navigation graph resource

2️⃣ add NavHostFragment 
• acts as a host for each fragment in the activity navigation graph as users move between pages, it automatically manages the stack 

3️⃣ add fragments to the navigation graph

4️⃣ connect fragments in the graph with actions
• adding and connecting screens don't actually do anything, they simply represent POSSIBLE pathways from one to fragment to another 

5️⃣ create onClickListener
💡the method they suggested in the course did not work!! 

6️⃣  find Navigation controller
• this is A CLASS used to manage navigation with our nav host fragment 
• the navigation host fragment is the parent in the view hierarchy of our current fragment aka the title screen fragment 
• which means that we can travel up the hierarchy and find it (title screen) from any view in our fragment even the play button! 

7️⃣  navigate with action 
PopTo NOT INCLUSIVE
• pops off everything on the back stack until it finds the referenced fragment transaction
PopTo Inclusive
• pops off everything on the back stack, including the referenced fragment transaction 

8️⃣  control animation with navigation listeners 
• to control where and when the drawer menu appears when 
• set inside onCreate() by calling it whenever the destination changes - when the id of our NavDestination matches the start destination of our graph, we’ll unlock the drawerLayout; otherwise, we’ll lock and close the drawerLayout.

NAVIGATION METHODS & FUNCTIONALITY 

📌 APP DRAWER NAVIGATION
• defaults to poping everything off the backstack except for the start destination 

📌 MENU NAVIGATION
• adds to the backstack from the current position

📌  DRAWER LAYOUT
• provides the foundation for the sliding behaviour of the navigation drawer

📌  NAVIGATION VIEW
• material design container that provides the look, feel, and functionality of the navigation drawer 

#Intent
INTENTS - are descriptions that the system uses to locate activities on behalf of applications 

📍EXPLICIT INTENT
• launches specific activity using the name of the target activity class  
• typically used only to launch other activities WITHIN the application 
• happens when you navigate to other activities in the navigation graph 

📍 IMPLICIT INTENT 
• provides an abstract description of the operation to be performed 
• most often used to launch activities that are exposed by other applications
• the system may not have any apps that can handle an implicit intent
• when multiple android apps can handle the same implicit intent - android will provide a pop-up list of compatible apps to let the user select the desired one to handle the request 

🌟importance: allows an app to request something from another app without having to know anything about that other app - when text is shared from our app with implicit intent - the app does not need to know the channel it is shared, just needs to know that there are applications/channels that can handle the "text-sharing" request

📌  INTENT ACTIONS 
• actions in each implicit intent and are DIFFERENT from those in the navigation graph 
• used here to describe the type of thing that is to be done 
• COMMON EXAMPLES = view(action_view), dial(action_dial), or edit(action_edit)

📌 INTENT CATEGORIES 
• adds a subtype to the intent-action to disambiguate the action
•  but aren't always used 
• EXAMPLE = the categories used along with the main entry point to launch available music players, mapping applications ... etc

📌  INTENT DATA TYPE (MIME DATA TYPE)
• implicit intents can include a data type like text or jpeg image which allows applications to be chosen based on what data type can be accepted
• EXAMPLE = sender intent  

📌  INTENT EXTRA
• used to provide arguments for the intent 
• some argument types have predefined keys like text 

⚠️  ALL ACTIVITIES MUST BE REGISTERED IN THE ANDROID MANIFEST TO BE LAUNCHED 
• explicit activities can be launched with a <activity> tag
• implicit activities require a <intent-filter> tag - it is used to expose that your activity can respond to an implicit intent with a certain action, category or type 
• if a given activity in the app doesn't have this <intent-filter> it will not launch in the app 
