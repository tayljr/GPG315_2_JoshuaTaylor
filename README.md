# Welcome to the GPG315_2_JoshuaTaylor wiki!

## Detailed usage instructions.
### CharacterBase:
Give each character a “CharacterBase” script.
Tick the bool “IsPlayer” if the character is the main player character
Give the character base a portrait sprite under the variable “CharPortrait”
Give the character base a name under the variable “CharName”
Set the character base’s “TextColour” to the colour best suited for the character

### Dialog JSON:
List of messages
 “TargetResponding” Bool 
   which character is speaking
 “Saying” String 
   what they are saying
Format:
 {
	"message": [
		{
			"targetResponding": false,
			"saying": "hi"
		},
		{
			"targetResponding": true,
			"saying": "hello there"
		}
	]
 }

### JSONReader:
Insert any JSON file, formatted like above
Converts it into a list of messages to be used in the dialog system

### ConversationAction:
“Agent” and “Target” are in conversation
Blackboard Variables:
 “Agent” CharacterBase
   The character who is talking
 “Target” CharacterBase
   Who they are talking to
 “Conversation” JSONReader
   list of messages and who is responding
 “agentDialogBox” TextMeshProUGUI
   The TMP text to change
 “agentName” TextMeshProUGUI
   The characters name
 “agentPortrait” Image
   The characters portrait box 
 “targetDialogBox” TextMeshProUGUI
   The other TMP
 “targetName” TextMeshProUGUI    
   The targets name 
 “targetPortrait” Image
   The targets portrait box
Gets the character's name, portrait and text colour from “Agent” and “Target”
Follows the messages in “Conversation”
Progress to the next message by pressing the space bar
After reaching the end of “Conversation” sets status as Success

### TalkAction (old)
“Agent” says “text” to “Target”
This system has been replaced by the ConversationAction although can still be used if preferred.
Blackboard Variables:
 “Agent” CharacterBase
   The character who is talking
 “text” string
   What they are saying
 “Target” CharacterBase
   Who they are talking to
 “agentDialogBox” TextMeshProUGUI
   The TMP text to change
 “agentName” TextMeshProUGUI
   The characters name
 “agentPortrait” Image
   The characters portrait box 
 “targetDialogBox” TextMeshProUGUI
   The other TMP
 “targetName” TextMeshProUGUI    
   The targets name 
 “targetPortrait” Image
   The targets portrait box
Gets the character's name, portrait and text colour from “Agent” and “Target”
Displays the text in “text”
pressing the space bar sets status as Success


### SampleDialogGraph:
Reads the messages from the JSON “SampleDialog”
NPC1 talks to Player
Reads the messages from the JSON “SampleDialog1”
NPC1 talks to NPC2

## Architectural overview and design decisions.
Building off Unity’s Behaviour Graph, my dialog system can integrate seamlessly with most other npc, or AI systems made using the behaviour graph. This also meant I did not need to create a custom editor as Unity’s Behaviour Graph had everything I needed to develop my plugin. 
A full conversation between two characters can be written up entirely in JSON and imported into this Dialog plugin. 

## Troubleshooting and common issues.
When creating the old system (TalkAction) and space bar was pressed, it triggered Success on all the future TalkAction actions. This was fixed by adding a delay of 0.1 secs after starting a new TalkAction.

## Future improvements and potential expansions.
Conversations with multiple characters in the same JSON file
Dialog choices
 Branching dialog
Localisation system
 Managing multiple languages
Optional text effects
 Bold
 Italics
 Size
 Strikethrough
 wiggle
