
Coming Soon
•	Objective
•	Service Scope
•	Assumption
•	Section 1: Coming Soon Program Data Structure 
o	1.1 Definition & Objectives
o	1.2 New Category Setup in PWH
o	1.3 Data Setup of Coming Soon Programs
o	1.4 API Enhancement
•	Section 2: Coming Soon Rail Setup in AMS
•	Section 3: Coming Soon Rail UI and UX Flow (Detail Page) 
o	Coming Soon Rail Display scenario : Coming Soon Rail Display (Row 23 Updated on 2023年8月9日 )
o	3.1 Coming Soon Rail
o	3.2 Coming Soon Program Detail Page (SVOD)
o	3.3 Coming Soon Program Detail Page (TVOD)
o	3.4 Entry Point to access Coming Soon Program Detail Page
o	3.5 Subscription Flow for Coming Soon Program
o	3.6 My Now Watchlist & History Handling for Coming Soon Program
o	3.7 Translation
•	Section 4: UI Interaction in Intermediate Period Between After Coming Soon Period and Before On-Air 
o	4.1 Coming Soon Rail
o	4.2 From Your Watchlist Rail
o	4.3 My Now Watchlist & My Now History
o	4.4 Program Detail Page
o	4.5 i-AD and Target Message
o	4.6 Hero Banner, inline Banner, Ad Hoc Banner
•	Section 5: UI Interaction when Coming Soon Program is On-air 
o	5.1 Coming Soon Rail
o	5.2 From Your Watchlist Rail
o	5.3 My Now Watchlist & My Now History
o	5.4 Program Detail Page
o	5.5 i-AD and Target Message
o	5.6 Translation
o	5.7 Hero Banner, inline Banner, Ad Hoc Banner
•	Section 6 Summary of UI Interaction
•	Section 7 Changes on subsidary video playback handling for existing On-Air Program (SVOD)
•	Section 8 UI Design Mockup
•	Section 9 Reporting 
o	9.1 Pixel log
o	9.2 Firebase log
Objective
1.	To promote upcoming key VOD programs to customers.
Service Scope
1.	A new rail named “Coming Soon” will be created on Home Screen.
2.	In Coming Soon, upcoming VOD programs, including both SVOD and TVOD, will be listed.
3.	User can view information such as program name, on-air time & synopsis of the upcoming VOD programs.
4.	User can interact with an upcoming VOD program to perform below actions:
1.	Watch trailer (if available);
2.	Subscribe to respective subscription pack for SVOD only; AND
3.	Add the program to Watchlist
5.	For upcoming VOD programs added to Watchlist, there will be indicator in From Your Watchlist rail when the programs are on-air later.
Assumption
1.	Selection of VOD programs to be shown in Coming Soon is by editorial picks.
2.	Coming Soon items will ONLY be available on:
1.	Coming Soon rail on Home Screen; AND
2.	My Now Watchlist
3.	Unless otherwise specified, Coming Soon feature shall NOT alter any existing logic in other existing UI pages/features.
4.	The availability on UI of Coming Soon programs is independent from “Display when asset ready” flag status in PWH.
1.	i.e. even if the Coming Soon program is set with “Display when asset ready = Y” in PWH, it is still eligible to be shown in Coming Soon as long as it fulfills below requirement
5.	It is assumed all 1st on-air schedules created per product level in PWH will NOT be deleted in any circumstances
6.	It is assumed that there will only be 1 Coming Soon Schedule per product.
7.	
8.	It is assumed that re-run programs are NOT eligible to be Coming Soon programs.
9.	It is assumed that program “On-Air” determination on all platform remain unchanged
1.	Asset readiness AND
1.	H1 : TV asset readiness
2.	U3 : TV asset readiness
3.	Now Player App : TV or OTT asset readiness
4.	Now Player Web : OTT asset readiness
2.	Current time is after earliest schedule start date
1.	The program will not “On-Air” before earliest schedule start date even asset is ready
10.	It is assumed that there will be NO bookmark saved for Coming Soon programs.
Section 1: Coming Soon Program Data Structure
1.1 Definition & Objectives
1.	A VOD program is defined as a Coming Soon program in product level in PWH, i.e.
1.	for VOD single program, the program will be defined as Coming Soon in product level.
2.	for VOD series, the entire series will be defined as Coming Soon in product level of the earliest available episode of the series, e.g. E1 in most cases.
2.	A VOD program is defined as a Coming Soon program if
1.	there is valid input in “Coming Soon(Home Menu)” Category Schedule in product level in PWH
3.	“Coming Soon(Home Menu)” Category Schedule will NOT be defined as the 1st on-air schedule of any product
4.	Below suggestion in data structure enhancement in PWH serves 3 purposes:
1.	to reduce repetitive manual input effort by editorial;
2.	to avoid confusion of 1st On-Air Schedule setup with coming soon schedule setup; AND
3.	to prevent re-run program to be shown in Coming Soon.
1.2 New Category Setup in PWH
1.	A new category named “Coming Soon(Home Menu)” will be created with below General parameters:
1.	Category Head/node = “TV : VODCatalog - VODCatalog”
2.	Category Tree attached (production) = VODCatalog > Search Exclude (Root) > Coming Soon(Home Menu)
3.	Category Tree attached (QA) = VODCatalog - root > Search Exclude (Root) > Coming Soon(Home Menu)
4.	Category ID = C202306290005730
5.	Category Type = “TV”
6.	Available UI = “New UI (U2, U3)”
7.	English Name (For UI display) = “Coming Soon(Home Menu)”
8.	Chinese Name (For UI display) = “Coming Soon(Home Menu)”
9.	English Name (For import) = “Coming Soon(Home Menu)”
10.	Chinese Name (For import) = “Coming Soon(Home Menu)”
11.	Category Library owner = L99998 : Reserved for Admin use
12.	Is Adult = N
13.	Check Subscription = N
14.	Status = ACTIVE
15.	Display Order = “1”
16.	Type (U2) = GROUP
17.	Is all Category = N
18.	Is always display = N
2.	CP assignment of category “Coming Soon(Home Menu)” will be as below:
1.	Coming Soon Category CP assignment.xlsx
3.	SubCustCat assigned under category “Coming Soon(Home Menu)” will be as below:
1.	RES
1.3 Data Setup of Coming Soon Programs
1.	To make a program eligible to become a Coming Soon program, a schedule under Category = “Coming Soon(Home Menu)” must be created
1.	in product level of VOD single product; OR
2.	in product level of the earliest available episode of the series, e.g. E1 in most cases
1.	Earliest available episode of the series is defined by the episode with the smallest PID in the series
2.	Any schedule under Category = “Coming Soon(Home Menu)” will NOT be counted as the 1st on-air schedule of the program
3.	Similar to existing schedule setup criteria, “Coming Soon(Home Menu)” Category Schedule will be with below parameters:
1.	Category = Coming Soon(Home Menu)
2.	Start Date = “As entered by user”
3.	End Date = “As entered by user”
1.	End Date must be later than Start Date
4.	Status = APPROVED
5.	Display Order = 0
1.	It is suggested to be set as “0” for all Coming Soon programs
2.	Even if the field is set as values other than “0”, this display order will NOT affected the final sorting order in Coming Soon rail
4.	To reserve flexibility for promoting upcoming episodes in VOD series, user can also enter “Coming Soon(Home Menu)” Category Schedule in episodes that are NOT the earliest available episode of the series, but these entries will NOT make the series eligible for Coming Soon
1.4 API Enhancement
1.	Subsequent to the setup of “Coming Soon(Home Menu)” Category under Category Tree = VODCatalog > Search Exclude (Root) >Coming Soon(Home Menu) , an independent pathway to get data from “Coming Soon(Home Menu)” Category out of Cat Engine will be set up
2.	Hero Banner, inline Banner, Ad Hoc Banner
1.	will be show up for Reference ID (PID) for
1.	current time within corresponding Coming Soon Schedule (PWH) AND ;
2.	current time within Banner Start Time and End Time (AMS) AND;
3.	contain the Coming Soon Program mandatory fields from PWH (https://now-tv.atlassian.net/wiki/spaces/NTV/pages/1839956036/Coming+Soon#Section-3%3A-Coming-Soon-Rail-UI-and-UX-Flow-(Detail-Page) point 3)
2.	will be supporting landing on Coming Soon Program Detail Page during the period defined in https://now-tv.atlassian.net/wiki/spaces/NTV/pages/1839956036/Coming+Soon#Section-3%3A-Coming-Soon-Rail-UI-and-UX-Flow-(Detail-Page)
3.	will be dismissed during the period defined in https://now-tv.atlassian.net/wiki/spaces/NTV/pages/1839956036/Coming+Soon#Section-4%3A-UI-Interaction-in-Intermediate-Period-Between-After-Coming-Soon-Period-and-Before-On-Air
4.	will be supporting landing on existing Program Detail Page during the period defined in https://now-tv.atlassian.net/wiki/spaces/NTV/pages/1839956036/Coming+Soon#Section-5%3A-UI-Interaction-when-Coming-Soon-Program-is-On-air
3.	Affected servers/engines are listed below: (TBC)
Section 2: Coming Soon Rail Setup in AMS
1.	Coming Soon rail is suggested to be created and operated in AMS;
2.	A new rail type, “Coming Soon Rail” is suggested to be created;
1.	“Coming Soon Rail” will be available on Home Screen v2.0, Kids Screen and Sports Guide 2
3.	“Coming Soon Rail” will include all Coming Soon programs with valid “Coming Soon(Home Menu)” Category Schedule as defined in PWH;
1.	For Coming Soon programs to be shown in Coming Soon rail, current time must be within the time values defined in “Coming Soon(Home Menu)” Category Schedule per program
4.	Suggested parameters in rail type “Coming Soon Rail”:
1.	Chinese display name (mandatory);
2.	English display name (mandatory);
3.	Platform (mandatory);
1.	options follow existing platform types, i.e. U3, NPX, ATV, EYE
4.	Maximum number of items (mandatory);
5.	Minimum number of items (mandatory):
1.	Default input value will be “0”;
2.	this field is to define minimum number of Coming Soon programs to be shown in Coming Soon rail;
3.	if total number of Coming Soon programs defined in PWH is less than this field, the entire Coming Soon rail will be hidden
6.	Manual Ordering (optional);
1.	this is a new optional field for “Coming Soon Rail”;
2.	user will input a list of PIDs as string for Coming Soon programs to be pinned at the front of Coming Soon rail:
1.	PID can be for both single VOD program and an episode in VOD series;
2.	e.g. if user wants program with PID 202303071797693 to be 1st item and another program with PID 202304061807971 to be 2nd item in Coming Soon rail, user will enter “202303071797693, 202304061807971” in this field
7.	Sub cust cat (mandatory)
1.	options follow existing sub cust cats
Section 3: Coming Soon Rail UI and UX Flow (Detail Page)
	Definition
Coming Soon Schedule	From PWH : “Approved” Schedule of Category “Coming Soon(Home Menu)”
Coming Soon Start Date	Coming Soon Schedule Start Date
Coming Soon End Date	Coming Soon Schedule End Date
1st On-Air Schedule	From PWH : “Approved” Earliest Schedule of Category other than “Coming Soon”, determined by Earliest Start Date
1st On-Air Schedule Start Date	1st On-Air Schedule Start Date
1st On-Air Schedule End Date	1st On-Air Schedule End Date
1.	After Coming Soon Rail is created in AMS, all Coming Soon Program to be shown in Coming Soon rail should be retrieved from PWH including those defined in Manual Ordering from AMS
1.	All Coming Soon Program displayed in Coming Soon Rail must with
1.	valid PID; AND
1.	any invalid PID input in Manual Ordering in AMS will be ignored;
1.	invalid PID input refers to any input that no product detail can be found in PWH
2.	current time is within Coming Soon Schedule; AND
1.	current time is before1st On-Air Schedule; OR
2.	current time is during 1st On-Air Schedule but asset not ready; OR
3.	without 1st On-Air Schedule
2.	For Program with Coming Soon Start Date later than 1st On-Air Schedule Start Date is not treated as Coming Soon Program, so will not appear in Coming Soon Rail AND no Coming Soon Description show up during Coming Soon Schedule.
3.	Coming Soon Program MUST contain the following mandatory fields from PWH; otherwise it will not create Coming Soon Program Detail Page and show up in Coming Soon Rail. This should also applies for Program listed in Manual Ordering in AMS.
1.	Library
2.	Program Title
3.	Portrait & Landscape Posters
Coming Soon Rail Display scenario : Coming Soon Rail Display (Row 23 Updated on 2023年8月9日 )
3.1 Coming Soon Rail
1.	Coming Soon rail will be available on Home Screen with number of rail item >= minimum of items defined in AMS.
2.	When the number of available Coming Soon Program is 0, or < minimum of items defined in AMS, the Coming Soon Rail will be hidden.
3.	Coming Soon Rail on Kids Home will ONLY display Coming Soon Program(s) which eligible to be displayed in Kids Profile, i.e. Kids Content, follow existing behaviour on Kids Home.
4.	Component of Coming Soon Rail Item
1.	Coming Soon Programs will be listed and displayed with Landscape and Portrait poster, Program Title, Coming Soon Description, Library Name, Classification, Synopsis, “Subscribed” label, “On Watchlist” label, similar with New Release Rail
1.	Program Title
2.	Coming Soon Description
1.	“Coming <1st On-Air Schedule Start Date>”
1.	current time is before 1st On-Air Schedule AND during Coming Soon Schedule
2.	date format
1.	refer to 0.6. Presentation Format, Short Form (Eng): DD Mmm and Short Forum (Chi): MM月DD日
2.	“Coming Soon”
1.	without 1st On-Air Schedule AND current time is during Coming Soon Schedule
2.	current time is during Coming Soon Schedule and 1st On-Air Schedule but Coming Soon Program asset not ready
3.	Coming Soon Description will be displayed as caption in NPX
 
3.	Library Name
4.	Classification 
5.	Synopsis (if available)
6.	“Subscribed” label
1.	Show “Subscribed” if user has subscribed to the corresponding library; if not, the label will be hidden
2.	This does not apply to TVOD
7.	“On Watchlist” label
1.	User can add the Coming Soon Program to watchlist by pressing “+” on RCU when the cursor is on any program poster on the rail. Then the “On Watchlist” label will show up immediately
2.	When user removes the item from Watchlist either from Program Detail Page or My Now Watchlist, the label will be dismissed
5.	Maximum and minimum number of items and Rail position will be following the setup from AMS.
1.	There will be NO “See All” button at the end of the rail
6.	Coming Soon Rail item will be dismissed by refresh when
1.	current time is after Coming Soon Schedule
2.	current time is during Coming Soon Schedule and 1st On-Air Schedule, with Coming Soon Program asset ready
7.	Display order
1.	If Manual ordering is null in AMS
1.	Coming Soon Program(s) will be sorted by those with 1st On-Air Schedule first in chronological order, follow by those which without
1.	If there are 2 Coming Soon Programs with the same 1st On-Air Schedule Start Date, they will be sorted by PID, from smallest to largest. 
2.	For those without 1st On-Air Schedule, they will be sorted by PID, from smallest to largest. 
2.	If Manual ordering is not null in AMS
1.	Coming Soon Rail will show the item listed in Manual ordering in AMS first, then by Coming Soon Program(s) will be sorted by those with 1st On-Air Schedule first in chronological order, follow by those which without (exclude those program listed in Manual ordering)
1.	If there are 2 Coming Soon Programs with the same 1st On-Air Schedule Start Date, they will be sorted by PID, from smallest to largest. 
2.	For those without 1st On-Air Schedule, they will be sorted by PID, from smallest to largest. excluding items listed in Manual Ordering)
3.	If total number of items exceed the maximum number of items defined in AMS, the extra Coming Soon Item will be hidden
Scenario	Manual ordering in AMS	Coming Soon Item in PWH order by 1st On-Air Schedule Start Date	Coming Soon Rail Display order (Maximum number of items : 10)
No input in AMS	-	2022001,2022003,2022002	2022001,2022003,2022002
Valid Coming Soon Program in Manual Ordering in AMS	2023003, 2023005, 2023001	2022001,2022003,2022002	2023003, 2023005, 2023001, 2022001,2022003,2022002
Invalid PID in Manual Ordering in AMS	2023003, 2023006, 2023001		2023003, 2023001
Coming Soon Program pass Coming Soon End Date	2023003, 2023009, 2023001	2022007,2022003,2022002	2023003,2023001,2022003,2022002
Any mandatory field is empty for program in Manual Ordering in AMS	2023003, 2023010, 2023001	2022009,2022003,2022002	2023003,2023001,2022003,2022002
Total number of Coming Soon Program exceed Maximum number of items	2023003, 2023005, 2023001,2023010,2023011,2023012	2022001,2022003,2022002,2022010,2022011,2022012	2023003, 2023005, 2023001,2023010,2023011,2023012,2022001,2022003,2022002,2022010
  
3.2 Coming Soon Program Detail Page (SVOD)
1.	Component (1st screen)
1.	Landscape and Portrait Poster
2.	Program Name
3.	Coming Soon Description
1.	Coming Soon Description
1.	“Coming <1st On-Air Schedule Start Date>”
1.	current time is before 1st On-Air Schedule AND
1.	during Coming Soon Schedule OR
2.	after Coming Soon Schedule
2.	date format
1.	refer to 0.6. Presentation Format, Short Form (Eng): DD Mmm and Short Forum (Chi): MM月DD日
2.	“Coming Soon”
1.	without 1st On-Air Schedule AND current time is during OR after Coming Soon Schedule
2.	current time is during Coming Soon Schedule and 1st On-Air Schedule but Coming Soon Program asset not ready
3.	current time is after Coming Soon Schedule and during 1st On-Air Schedule, but Coming Soon Program asset not ready
3.	Dismiss by refresh when Coming Soon Program is On-Air
1.	current time is during Coming Soon Schedule and 1st On-Air Schedule, with Coming Soon Program asset ready
2.	current time is after Coming Soon Schedule and and during 1st On-Air Schedule, with Coming Soon Program asset ready
4.	Synopsis (if available)
1.	Press “OK” to view the long synopsis
5.	Edition/Version (if available)
6.	Classification
7.	Encoding 4K (if Y in PWH)
8.	Support 5.1 Audio (if Y in PWH)
9.	Number Of Episode (if available)
10.	Audio Language (if available)
11.	Subtitle Language (if available)
12.	Contains Indirect Advertising (if Y in PWH))
13.	Library Logo
14.	“Watch [subsidiary type]” button, “Subscribe” button and “Add to Watchlist” button
1.	Refer to the table in Section 3.2.3
 
 
2.	Component (2nd Screen)
1.	“Trailer & Extras” Rail (Refer to the table in 3.2.3)
2.	“Episode” Rail
1.	there will be NO episode rail in Coming Soon Detail page
3.	“Other Seasons” Rail (if available)
1.	this rail will NOT contain any Coming Soon program as rail item
4.	“Recommended” Rail
1.	this rail will NOT contain any Coming Soon program as rail item
5.	“Cast & Crew” (if available)
1.	When user clicks any cast and crew option and goes to NowTV Search, NO Coming Soon program will appear as search result
6.	No Schedule End Date will be shown
7.	Platform
8.	Season no. (if available)
9.	Number Of Episode (if available)
3.	Handling of subsidiary
1.	Refer to H1 & U3CTA Button Assignment & Now Player CTA Button Mapping Table , CTA button and “Trailer & Extras” rail handling will be as follow
Entitlement	Add to Watchlist	Number of subsidiary	H1 & U3 CTA Button 1	H1 & U3 CTA Button 2	H1 & U3 CTA Button 3	“Trailer & Extras” Rail	Now Player 1st Row CTA Button 1	Now Player 2nd Row CTA Button 1	Now Player 2nd Row CTA Button 2	Now Player 2nd Row CTA Button 3
N	N	1	Subscribe	Watch [subsidiary type]	Add to Watchlist	N	Subscribe	Trailer	Add to Watchlist	Share
Y	N	1	Watch [subsidiary type]	Add to Watchlist		N		Trailer	Add to Watchlist	Share
N	Y	1	Subscribe	Watch [subsidiary type]	On Watchlist	N	Subscribe	Trailer	On Watchlist	Share
Y	Y	1	Watch [subsidiary type]	On Watchlist		N		Trailer	On Watchlist	Share
N	N	>= 2	Subscribe	Add to Watchlist		Y	Subscribe	Trailer	Add to Watchlist	Share
Y	N	>= 2	Add to Watchlist			Y		Trailer	Add to Watchlist	Share
N	Y	>= 2	Subscribe	On Watchlist		Y	Subscribe	Trailer	On Watchlist	Share
Y	Y	>= 2	On Watchlist			Y		Trailer	On Watchlist	Share
3.3 Coming Soon Program Detail Page (TVOD)
1.	Component (1st screen)
1.	Landscape and Portrait Poster
2.	Program Title
3.	Coming Soon Description (same with Coming Soon Detail Page(SVOD), Section 3.2.1.c.i)
4.	Synopsis (if available)
1.	Press “OK” to view the long Synopsis
5.	Edition/Version (if available)
6.	Classification
7.	TV Asset Available (4K) (if available)
8.	Support 5.1 Audio (if available)
9.	Duration (mins)
10.	Audio Language (if available)
11.	Subtitle Language (if available)
12.	Contains Indirect Advertising (if available)
13.	Library Logo
14.	“Watch [subsidiary type]” button and “Add to Watchlist” button
1.	There will be NO “Rent” button in Coming Soon Detail Page for TVOD
 
2.	Component (2nd Screen)
1.	“Trailer & Extras” Rail
2.	“Recommended” Rail
1.	this rail will NOT contain any Coming Soon program as rail item
3.	“Cast & Crew” (if available)
1.	When user clicks any cast and crew option and goes to NowTV Search, NO Coming Soon program will appear as search result
4.	Platform
5.	No Schedule End Date
3.	Handling of subsidiary
1.	Refer to H1 & U3CTA Button Assignment & Now Player CTA Button Mapping Table , CTA button and “Trailer & Extras” rail handling will be as follow
2.	After user presses BACK during trailer playback OR after trailer playback is finished;
1.	VOD rental flow will NOT be activated; AND
2.	user will be guided back to Coming Soon Detail page, with cursor at its last position
Add to Watchlist	Number of subsidiary	CTA Button 1	CTA Button 2	“Trailer & Extras” Rail	Now Player 1st Row CTA Button 1	Now Player 2nd Row CTA Button 1	Now Player 2nd Row CTA Button 2	Now Player 2nd Row CTA Button 3
N	1	Watch [subsidiary type]	Add to Watchlist	N		Trailer	Add to Watchlist	Share
Y	1	Watch [subsidiary type]	On Watchlist	N		Trailer	On Watchlist	Share
N	>= 2	Add to Watchlist		Y		Trailer	Add to Watchlist	Share
Y	>= 2	On Watchlist		Y		Trailer	On Watchlist	Share
3.4 Entry Point to access Coming Soon Program Detail Page
1.	Coming Soon Rail
2.	My Now Watchlist
3.	i-Ad & Target Message
1.	i-Ad and Target Message will be able to use the PID or any other URL link (if available) to land to Coming Soon Program Detail Page
2.	It is suggested to schedule Coming Soon program i-Ad Campaign within Coming Soon Start Date and End Date to ensure the smooth landing on Coming Soon Program detail page and process the Coming Soon Program Subscription Flow
4.	Hero Banner, inline Banner, Ad Hoc Banner
1.	For banner eligable to be shown up and click to land on Coming Soon Program detail page, it should follow the critieria (Coming Soon Schedule set up and mandatory field) mentioned in Section 3 point 1, 2, & 3, similar with Coming Soon Rail.
2.	It is assumed that during initial launch, Coming Soon Program will will only be set up in Home Screen Hero Banner, inline Banner or Ad Hoc Banner
3.5 Subscription Flow for Coming Soon Program
For SVOD
1.	Subscription flow for Coming Soon Program will be same as normal VOD program with on-air asset, with a different set of text.
2.	Entry Point to Coming Soon Program subscription page
1.	Click “Subscribe” button in Coming Soon Program detail page; OR
2.	Enhancement for U3 & H1 ONLY, subsidiary video playback complete/exit/back for library without entitlement, applying to both Coming Soon SVOD and On-Air SVOD program 
1.	This entry point is unavailable on NPX 
3.	Coming Soon Program Subscription Page
1.	Text Message
1.	[Program Title] will be available soon!
To enjoy it and more, subscribe to
1.	If the number of characters of the message exceeds the display limit, follow existing pack subscription page truncation rule
 
2.	 
For Now Player, it is expected to land to Now TV website with Coming Soon Program Description (TBC)
3.	Upon success subscription
1.	Text Message
1.	Success! Your’ve successfully subscribed to [Pack Name]. We’re currently processing your order. You can watch the newly subscribed programmes on Now TV or Now Player! [Program Title] is added to your Watchlist for your easy access once it's available.
2.	For U3 & H1 ONLY, the program will be automatically added to watchlist
1.	User can find the Coming Soon Program in My Now Watchlist
2.	Coming Soon Program will not show up in “From Your Watchlist Rail” if asset is NOT ready and before 1st On-Air Schedule Start Date
3.	This feature is unavailable on NPX
4.	  
For TVOD
1.	After subsidiary video playback complete/exit/back for library, it should not direct user to “Rent” page 
3.6 My Now Watchlist & History Handling for Coming Soon Program
1.	My Now Watchlist
1.	Coming Soon Description (e.g. “Coming 17 Apr”) will replace the existing caption position after Coming Soon Start Date and before 1st On-Air Schedule
1.	Same with Coming Soon Detail Page(SVOD), Section 3.2.1.c.i
2.	Wording limit and Truncation Rules will follow existing setup.
 
2.	Coming Soon Program also supports “Long Press OK to Remove”
3.	My Now Watchlist housekeeping rules for Coming Soon Program
1.	If Program is assigned with ONLY Coming Soon Schedule, and no 1st On-Air Schedule is assigned within 60 days after Coming Soon Schedule End Date, the program will be dismissed from My Now Watchlist
1.	If 1st On-Air Schedule is assigned within 60 days after Coming Soon Schedule End Date, it will follow the case handling of having both Coming Soon Schedule and On-Air Schedule
2.	If Program is assigned with both Coming Soon Schedule and 1st On-Air Schedule, after all valid On-Air Schedule(s) expire and without any alternative program, the program will be dismissed from My Now Watchlist, follow existing behaviour
4.	H1 Handling : For Coming Soon Program without 1st On-Air Schedule
1.	Under “Latest” and “Expiring”, the corresponding program will be placed at the bottom of the list as without any On-Air Schedule, following existing behaviour
5.	U3 & Now Player Handling
1.	For Coming Soon Program, it should shown in both “All” & “Coming Up” tab
2.	Display order will be following existing behaviour
3.	For Coming Soon Program displayed in Now Player, it is expected to shown as program available to play with cursor on the right
1.	Apply to both library with or without entitlement, and TVOD for both “All” and “Coming Up” tab
 
6.	Grouping by CID
1.	Coming Soon Program will not be grouped by CID with Coming Soon Program or On-Air Program, i.e. Coming Soon Program with the same CID will be displayed separately in My Now Watchlist
2.	My Now History
1.	It will not display the viewing record of any subsidiary for both Coming Soon Program and On-Air Program, follow existing behaviour
3.7 Translation
	English	Chinese
Rail Title	Coming Soon	即將上架
Coming Soon Description (with 1st On-Air Schedule start date)	Coming <1st On-Air Schedule start date>
e.g. Coming 17 Apr	將於<1st Schedule Start Date> 上架
e.g. 將於 4 月 17 日上架
Coming Soon Description (without date)	Coming Soon	即將上架
Coming Soon Program Subscription Page	<Program Name> will be available soon!
To enjoy it and more, subscribe to	<Program Name> 即將上架！
訂購及預設觀看列表，同時發掘更多精彩節目
Coming Soon Program Pack Subscription Success Page	We’re currently processing your order. You can watch the newly subscribed programmes on Now TV or Now Player!
<Program Title> is added to your Watchlist for your easy access once it's available.	我們現正處理你的訂單。訂購成功後，你可透過 Now TV 機頂盒或 「Now 隨身睇」觀看新訂購的組合內容！
已將<Program Title> 加入觀看列表，方便你於節目上架後，隨時觀看。
Section 4: UI Interaction in Intermediate Period Between After Coming Soon Period and Before On-Air
1.	This section lists the UI interaction of different UI features when a Coming Soon program :
1.	has exceeded its Coming Soon Schedule, i.e. current time is beyond Coming Soon End Date; AND
1.	before 1st On-Air Schedule OR
2.	during 1st On-Air Schedule but asset is NOT yet ready OR
3.	1st On-Air Schedule is NOT available
2.	    
2.	This period will be named as intermediate period in this requirement
4.1 Coming Soon Rail
1.	When any program on the Coming Soon Rail reaches its Coming Soon End Date, the program will be dismissed from Coming Soon Rail after refresh of Home Screen;
1.	When the number of availbale Coming Soon Program < minimum of items defined in AMS, the Coming Soon Rail will be hidden.
2.	When user click on any program exceeding the Coming Soon End Date before Home Screen refresh, show the Program Detail Page with Coming Soon Description (Section 4.4)
4.2 From Your Watchlist Rail
1.	This rail only show asset ready program, so any Coming Soon program added by user will NOT show up in intermediate period.
1.	Coming Soon program will be available on From Your Watchlist rail until its asset is ready and it has reached its 1st On-Air Schedule (refer to Section 5.2).
4.3 My Now Watchlist & My Now History
1.	My Now Watchlist
1.	Coming Soon Program caption logic (section 3.2.1.c.i) will be applied during intermediate period for Coming Soon programs;
2.	In order to show Coming Soon Program in My Now Watchlist in intermediate period, “Display when asset ready” in PWH will be bypassed for Coming Soon Program until it is On-Air. 
3.	H1 Handling : For Coming Soon Program without 1st On-Air Schedule
1.	Under “Latest” and “Expiring”, the corresponding program will be placed at the bottom of the list as without any On-Air Schedule, following existing behaviour
4.	U3 & Now Player Handling
1.	For Coming Soon Program, it should shown in both “All” & “Coming Up” tab
2.	Display order will be following existing behaviour
3.	For Coming Soon Program displayed in Now Player, it is expected to shown as program available to play with cursor on the right
2.	My Now History
1.	It will not display the viewing record of any subsidiary for both coming soon program and on-air program, follow existing behaviour
4.4 Program Detail Page
1.	VOD Detail Page in intermediate period will be identical to existing VOD Detail Page for Coming Soon programs.
2.	Coming Soon Description handling determine by current time 
1.	“Coming Soon”
1.	during 1st On-Air Schedule but asset is NOT yet ready OR
2.	1st On-Air Schedule is NOT available
2.	“Coming <1st On-Air Schedule Start Date>”
1.	before 1st On-Air Schedule 
3.	There will be NO “Rent” button for TVOD.
1.	After subsidiary video playback complete/exit/back for library, it should not direct user to “Rent” page.
4.	“Subscribe” button will be available, and undergo Coming Soon Program subscription flow (Refer to Section 3.5) .
5.	No Schedule End Date will be shown
4.5 i-AD and Target Message
1.	i-AD and Target Message should be able to use the same PID or link to land to Coming Soon Program Detail Page for Coming Soon Program in intermediate period.
4.6 Hero Banner, inline Banner, Ad Hoc Banner
•	will be dismissed for Reference ID (PID) which current time is during intermediate period
o	will shown up next banner based on existing logic
Section 5: UI Interaction when Coming Soon Program is On-air
1.	This section lists the UI interaction of different UI features when:
1.	a Coming Soon program has been on-aired; AND
2.	current time is within its 1st On-Air schedule as set in PWH
1.	even if the program is still within Coming Soon period, all UI interaction will follow this section as long as it fulfills the above criteria
2.	In case, the program is on-air earlier than scheduled, such that current time is during both Coming Soon Schedule and 1st On-Air Schedule
1.	UI features update will depend on each platform existing refresh mechanism
1.	E.g. If user stay at Coming Soon Program Detail Page before the program on-air, and watch the subsidary program or visit other program detail page in the “Recommended” rail, then program is on-air and user click “Back” button
1.	H1 : will not be refreshed and stay at Coming Soon Program Detail Page
2.	U3, Now Player Web & App : will be refreshed to On-Air Program Detail Page
5.1 Coming Soon Rail
1.	On-air program will NOT be shown in Coming Soon rail in usual cases;
2.	When user click on any on-air program exceeding the Coming Soon End Date before Home Screen refresh, show the Program Detail Page without Coming Soon Description (Section 5.4)
5.2 From Your Watchlist Rail
1.	When Coming Soon Program in Watchlist become on-air and is within its 1st On-Air schedule, this item will be shown as the 1st item in “From Your Watchlist Rail” after Home Screen refresh;
2.	The caption will be showing “Available Now” for 7 days from 1st On-Air schedule Start Date , which will always replace existing caption, except case mentioned in 3a
3.	The caption will resume and follow existing behaviour, e.g. “New:E1” / “Latest:E2”/”Subscribe”/with Poster Tag/”Ends” if current time is 7 days after 1st On-Air Schedule Start Date
1.	if user has rented or start watching the single program with valid bookmark within 7 days after 1st On-Air Schedule Start Date, “Rented.Exp.” / “Resume” will override “Available Now” in the caption 
1.	If user has finished the single product or rental period has passed within 7 days after 1st On-Air Schedule Start Date, caption will resume as “Available Now” upon refresh
2.	if user has rented the series after 1st On-Air Schedule Start Date, “Rented.Exp.” will override “Available Now” in the caption
1.	If user has finished the series or rental period has passed within 7 days after 1st On-Air Schedule Start Date, caption will resume as “Available Now” upon refresh
 
5.3 My Now Watchlist & My Now History
1.	My Now Watchlist
1.	when Coming Soon program is on-aired, the caption of the Program will be updated to “Available Now”
2.	Caption handling always refer to https://now-tv.atlassian.net/wiki/spaces/NTV/pages/1839956036/Coming+Soon#5.2-From-Your-Watchlist-Rail point 2 and 3
3.	For H1, It is expected that it only updated the ordering in the filtering “Added”, no change in display logic in “Latest” or “Expiring”
4.	position of the items will be same as those in “From Your Watchlist” rail
5.	 
6.	U3 & Now Player Handling
1.	For On-Air Program, it should shown in both “All” & “Watch Now” tab
2.	Display order will be following existing behaviour
3.	For On-Air Program displayed in Now Player, 
1.	For series with/without entitlement, single program without entitlement, unrent TVOD: It is expected to shown as program available to play with cursor on the right for 7 days from 1st On-Air Schedule Start Date in both “All” & “Watch Now” tab
2.	For single program with entitlement, Rented TVOD : It is expected to shown with “Play” button in both “All” & “Watch Now” tab
 
3.	After 7 days, it is expected to follow existing behaviour for library with or without entitlement, rented or not yet rented TVOD.
 
2.	My Now History
1.	Once user has watched any Master video for the program, the item will be shown in My Now History, follow existing behaviour
5.4 Program Detail Page
1.	VOD Detail Page will change to be the existing VOD Detail Page for on-air programs.
2.	No Coming Soon Description will be displayed.
3.	Subscription flow triggered by clicking “Subscribe” button OR subsidiary video playback complete/exit/back for library without entitlement (H1 & U3 Only, not available for NPX):
1.	Text Message
1.	To enjoy [Program Title] and more, subscribe to
2.	Success! You’ve Successfully Subscribed to [Pack Name]. We’re currently processing your order. You can watch the newly subscribed programmes on Now TV or Now Player ! You’ll see programmes and catalogues on your homescreen as soon as it’s available.
4.	For TVOD
1.	After subsidiary video playback complete/exit/back for the program, it should be able to direct user to “Rent” page similar to On-Air Program
5.	Schedule End Date will be shown follow exsiting behaviour
5.5 i-AD and Target Message
1.	i-AD and Target Message logic and flow will be same as existing behaviour of on-air programs
2.	It is suggested to schedule on-air Program i-Ad Campaign after Earliest Schedule Start Time to ensure the smooth landing on Program detail page and process the original Program Subscription Flow.
5.6 Translation
	English	Chinese
On-Air Program Caption	Available Now	現已上架
5.7 Hero Banner, inline Banner, Ad Hoc Banner
•	will be shown up for PID which current time is during On-Air Schedule
o	onclick will land on On-Air Program Detail Page
Section 6 Summary of UI Interaction
1.	Apply for both Coming Soon Program in PWH and Manual Ordering Program in AMS
UI Feature	Within Coming Soon Start Date and End Date (Section 3)	After Coming Soon End Date, i.e. in intermediate period (Section 4)	Asset ready & within 1st schedule (Section 5)
Coming Soon Rail
Coming Soon Program are shown
Program NOT found
Program NOT found

From Your Watchlist Rail
Program NOT found
Program NOT found
Items with master programs are shown if user has added to My Now Watchlist

From Your Watchlist Rail - Caption	-	-	All Coming Soon Program Program Caption will be shown as below, for 7 days from 1st On-Air schedule Start Date , which will always replace existing caption , except the special case mentioned in the bottom
•	“Available Now”
the caption will resume and follow existing behaviour if current time is 7 days after 1st On-Air Schedule Start Date 
•	Follow existing behaviour, “New:E1” /“Latest:E2”/”Subscribe”/with Poster Tag/”Ends”
________________________________________
Special case:
1.	if user has rented or start watching the single program with valid bookmark within 7 days after 1st On-Air Schedule Start Date, “Rented.Exp.” / “Resume” will override “Available Now” in the caption 
1.	If user has finished the single product or rental period has passed within 7 days after 1st On-Air Schedule Start Date, caption will resume as “Available Now” upon refresh
2.	if user has rented the series or start watching with valid bookmark within 7 days after 1st On-Air Schedule Start Date, “Rented.Exp.” will override “Available Now” in the caption
1.	If user has finished the series or rental period has passed within 7 days after 1st On-Air Schedule Start Date, caption will resume as “Available Now” upon refresh
My Now Watchlist
Coming Soon Program are shown	Coming Soon Program are shown	Items with master programs are shown

My Now Watchlist - Caption	Coming Soon Description	Coming Soon Description	Follow From Your Watchlist Rail - Caption
My Now History
Not Applicable
Not Applicable
Items with master programs are shown (Once user has watched any master program)

My Now History - Caption
-	-	Follow From Your Watchlist Rail - Caption
Search
Program NOT found
Program NOT found
Items with master programs are shown

On Demand Catalog
Program NOT found
Program NOT found
Items with master programs are shown

On Demand Catalog - Caption	-	-	Follow From Your Watchlist Rail - Caption
Program Detail Page
•	“Other Seasons” Rail
•	“Recommended” Rail
•	“Cast & Crew” Rail - Click result	Program NOT found	Program NOT found	Items with master programs are shown
Program Detail Page - Coming Soon Description	Coming Soon Program caption logic (section 3.2.1.c.i)	Coming Soon Program caption logic (section 3.2.1.c.i)	NO Coming Soon Description
Program Detail Page - Schedule End Date	N/A	N/A	Follow Existing behaviour
Subscription Flow Text Message	Text Message for Coming Soon Program	Text Message for Coming Soon Program	Original Text Message
Hero Banner, inline Banner, Ad Hoc Banner	Click to land on Coming Soon Program Detail Page	Dismiss, and shown up next banner based on existing logic	Click to land on Program Detail Page
Section 7 Changes on subsidary video playback handling for existing On-Air Program (SVOD)
Refer to Section 3.5 & Section 5.4, subsidiary video playback complete/exit/back for library without entitlement (H1 & U3 Only) for existing On-Air Program (SVOD) will also direct to Pack Subscription Page under this enhancement.
Section 8 UI Design Mockup
https://www.figma.com/file/Bp0qIrrXDPUMeF40lbPkoC/%5BReview%5D-Sponsor-Text-%26-Coming-Soon-Display?type=design&node-id=96-38960&t=mSYpIfqCflgF98Tz-0
Section 9 Reporting
9.1 Pixel log
1.	Basic logging logic of Coming Soon rail on Home Screen is expected to be similar to other existing rails on Home Screen on all platforms, including U3, H1 & NPX
	User Story	Importance	Acceptance Criteria
1	As a TV / NPX user, I want to track the hit rate of the Coming Soon rail item, so I can review the usage of rail item	MUST HAVE	1.	Action log of rail item will be required;
1.	It is required to include the rail position, rail title (in form of EN) in the hit count to indicate selected item coming from which rail;
2.	It is required to include the ID of item: product ID / Series ID / library ID to indicate which program had been selected;
3.	It is required to include the profile ID in the hit count;
2.	Action Tracking: It is required to track the customer action path from Coming Soon rail to Coming Soon detail page;
1.	The Coming Soon detail page will have referrer tracking “refer_page”, which indicating it is accessed from Coming Soon rail in Home Screen;
2.	When user press the product detail page action button: “SUBSCRIBE”, there will be referrer “refer_page” to indicate the action from Coming Soon rail in Home Screen
2	As a TV / NPX user, I want to distinguish Coming Soon detail page from general detail page.	MUST HAVE	1.	Besides usual log items of general detail page, one more NEW attribute will be logged:
1.	“coming_soon = Y/N”
2.	For general detail page, coming_soon = N
3.	For Coming Soon detail page, coming_soon = Y
3	As a TV user, I want to have visit count on Coming Soon rail, so I can track the user browsing rate of rail	MUST HAVE	1.	It is required to log user rail navigation before leaving Coming Soon rail;
2.	For example,
If the customer access the rails on Home Screen in following sequence: [From Your Watchlist] > [Coming Soon] > [Top 20] > [Coming Soon] 
It is required to track user had visited From Your Watchlist] and [Top 20] rail once, and [Coming Soon] in twice
3.	If customer presses “Back To Top” button at the bottom of Home Screen and goes back to Hero Banner, browsing rate of Coming Soon rail will not be counted twice
4.	If customer selects any Coming Soon program in Coming Soon rail and enters Coming Soon detail page, and then presses BACK to return to Coming Soon rail, browsing rate of Coming Soon rail will ONLY be counted once
5.	This requirement does NOT apply to NPX
NPX pixel log:
1.	NPX pixel log will use existing logging events to capture Coming Soon rail usage on Home Screen
2.	Rail name “Coming Soon” will be reflected as parameters
Pixel log	 Code
NPX App - Home Menu - Select Rail Item Click (Android)	http://nowplayer.now.com/plog.gif?page=AndroidNPXAppHKHomeMenuSelectRailItemClick&railListTitle=Coming%20soon&railListId=ams_202201030000295&productID=202308080108871&productType=product&row=1&position=0&lang=zh&UID=50E706DC-6F37-4111-BEB2-6868E8EAEDF3&osversion=16.4.1&nowid=iptvmat03@gmail.com&fsa=60086575&mupID=3061&profileType=NORMAL&mupName=1&mupIconID=color01&ver=7_46_0
NPX App - Home Menu - Select Rail Item Click (Android Tab)	http://nowplayer.now.com/plog.gif?page=AndroidTabNPXAppHKHomeMenuSelectRailItemClick&railListTitle=Coming%20soon&railListId=ams_202201030000295&productID=202308080108871&productType=product&row=1&position=0&lang=zh&UID=50E706DC-6F37-4111-BEB2-6868E8EAEDF3&osversion=16.4.1&nowid=iptvmat03@gmail.com&fsa=60086575&mupID=3061&profileType=NORMAL&mupName=1&mupIconID=color01&ver=7_46_0
NPX App - Home Menu - Select Rail Item Click (iPad)	http://nowplayer.now.com/plog.gif?page=iOSiPadNPXAppHKHomeMenuSelectRailItemClick&railListTitle=Coming%20soon&railListId=ams_202201030000295&productID=202308080108871&productType=product&row=1&position=0&lang=zh&UID=50E706DC-6F37-4111-BEB2-6868E8EAEDF3&osversion=16.4.1&nowid=iptvmat03@gmail.com&fsa=60086575&mupID=3061&profileType=NORMAL&mupName=1&mupIconID=color01&ver=7_46_0
NPX App - Home Menu - Select Rail Item Click (iOS)	http://nowplayer.now.com/plog.gif?page=iOSNPXAppHKHomeMenuSelectRailItemClick&railListTitle=Coming%20soon&railListId=ams_202201030000295&productID=202308080108871&productType=product&row=1&position=0&lang=zh&UID=50E706DC-6F37-4111-BEB2-6868E8EAEDF3&osversion=16.4.1&nowid=iptvmat03@gmail.com&fsa=60086575&mupID=3061&profileType=NORMAL&mupName=1&mupIconID=color01&ver=7_46_0
NPX App - Home Menu - Select Rail Item Click (Web)	http://nowplayer.now.com/plog.gif?page=NPXWebHKHomeMenuSelectRailItemClick&railListTitle=Coming%20soon&railListId=ams_202201030000295&productID=202308080108871&productType=product&row=1&position=0&lang=zh&UID=50E706DC-6F37-4111-BEB2-6868E8EAEDF3&osversion=16.4.1&nowid=iptvmat03@gmail.com&fsa=60086575&mupID=3061&profileType=NORMAL&mupName=1&mupIconID=color01&ver=7_46_0
9.2 Firebase log
1.	NPX firebase log will use existing logging events to capture usage of Coming Soon rail on Home Screen as well as Coming Soon Detail page
1.	PWH usual report to exclude Coming Soon cat
2.	How many items on rail at a specific time
3.	PID click per FSA
