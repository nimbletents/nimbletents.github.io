## Content
{:.no_toc}

* ToC
{:toc}


## Introduction

Social media platforms enable connection and sharing among friends, family and colleagues, while offering unprecedented opportunities for getting ideas out to much larger audiences. Political events such as the Arab Spring and social movements like Black Lives Matter show what important work is possible with social media at scale.

At the same time social media can be used to spread messages of intolerance, harassment and hate, as we’ve seen in the rhetoric surrounding Gamergate and the 2016 presidential race. Women, members of marginalized communities, and activists often find themselves the target of trolling and organized groups that attempt to shut down and silence their work. 

The Maryland Institute for Technology in the Humanities (MITH) organized a Night Against Hate 13th  October 2016 to gather and learn how to investigate and work to resist hate speech in social media. At the event, we spent two hours working to collaboratively link groups and individuals documented in the Southern Poverty Law Center’s Extremist Files, a list of known hate groups, to their respective Twitter accounts in order to:

- assist social media researchers who are studying the ways that these groups are operating online
- provide an opportunity for folks to respond constructively to the rising tide of hate we are witnessing in online and offline spaces
- create a Twitter block list that would allow individuals to prevent extremists identified by the SPLC from tweeting into their timeline. 

## Foundations 

Given the extreme rhetorics of intolerance, racism, and bigotry within these groups, The Night Against Hate centered participant self-care and attention to best practices for online activism. 

To prepare for *The Night Against Hate*, MITH organized a general interest meeting to encourage scholars and potential participants to discuss what research may emerge from connecting Southern Poverty Law Center’s Extremist Files entries with social media accounts. The interest meeting helped connect those on campus already engaged with - or had an interest in - online extremism research, social media analysis, and/or online rhetoric. Additionally, the interest meeting raised potential pitfalls or risks in doing this work and offered established researchers the opportunity to share their best practices for research and self-care. Finally, the interest meeting helped guide our decisions about what products we could create at the event that would be useful to researchers and individuals: 

- A CSV dataset that documents the connections between known extremists and their social media accounts which could be used in analyzing Twitter data and networks.
- A block list that users could import into their Twitter account in order to prevent hate speech from entering their timeline.

The pre-event interest meeting stressed a need to carefully attend to privacy and exposure, particularly participants who have not engaged with online activism previously. Unless precautions were taken social media sites may track browsing behavior as indicative of genuine interest and use this information for recommendation and classification purposes.

- Use Tor browser if desired, 
- Alternatively use Chrome in Incognito mode, or Firefox Private Browsing.
- Clear cache periodically.
- Online security tips: https://hackblossom.org/cybersecurity/ 
- Semi-private DH Slack channel - chosen because we wanted a semi-private channel for communication that had an explicit Code of Conduct
 
The code for collecting the Southern Poverty Law Center data and for creating the block list from the Google Sheet is available on Github.

## During the event

The Night Against Hate brought together over 50 local and remote participants. We worked in short 30 min sprints with 10 minute breaks for reflection and conversation. We strongly encouraged participants to work in groups and to pay attention to how the work affected participants well-being. Small groups helped participants verify information, ask questions, and support each other.

Logistically, we used Google Sheets and the Slack channel to link and verify 89 of the 169 individuals and groups present in the Extremist Files. Both Google Sheets and Slack helped us stay organized and verify information. The short sprints helped participants gather important information without staying in the muck for long periods of time, while the reflection periods offered time to talk through how participants were feeling as they engaged with tracking hate speech online or to share emerging questions or concerns. 

At the beginning of the event, we shared the contexts for organizing The Night Against Hate, how the event was organized into sprints, provided instructions on how to use the Southern Poverty Law Center’s Extremist Files, how to locate and collect YouTube, Facebook and Twitter handles. We offered suggestions for online privacy and requested participants share their best practices.

## After the event

After the event, MITH shared a blog post with instructions on how to use the block list which was created from the efforts of The Night Against Hate. We were delighted that participants collected Twitter handles and Facebook, YouTube, Tumblr, and websites where possible. The full results of the night’s efforts can be found in the Google Sheet. 

To use the block list users needed to:

- Right-Click on this link to the block list and select Save Link As or your browser’s equivalent.
- Go to your Twitter Settings, select Blocked Accounts in the menu on the left, click Advanced Options and then select Import a List from the dropdown.
- When you click Attach a file to upload you will prompted to provide the location of the block list file you downloaded.
- Once you’ve submitted the file you will see a list of the Twitter accounts present in the block list and have the opportunity to select/deselect them.
- Click Block.

A few more things about the block list are worth noting, the block list itself must contain Twitter user identifiers (numbers) instead of the Twitter handles. Ed Summers wrote a program to scrape the handles from the Google Spreadsheet and fetch the user identifiers from the Twitter API. We did consider making the block list available using the BlockTogether service, which would allow the list to be shared more easily. However BlockTogether associates the block list with a given user’s account, and we didn’t want to potentially mix the Extremist Files accounts with our other blocked accounts. Finally, the block list file of numeric identifiers cannot end with a newline or the Twitter import mechanism will not work.

Tools such as Google Sheets, Slack, private browsers, and GitHub proved to be very useful for this Rapid Response Research project. Google Sheets in particular worked well as a real time, data integration platform that provided visual feedback of what was being worked on by who. It also allowed for the data to easily be exported as CSV and used in other settings as data. Slack was useful for our remote participants, however we did find that given the sensitive nature of this research, and the emotional labor involved, that it was very useful for us to gather in the same physical space to do the work. In some cases remote participants reported that they felt isolated and alone looking at this particular material. We found that solidarity travels easiest when people are face to face.



