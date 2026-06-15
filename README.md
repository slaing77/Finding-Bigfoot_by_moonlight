# FINDING BIGFOOT BY MOONLIGHT								
Analysis by S.R. Laing	
<p>I've been tooling around with UFO data scraped from NUFORC and generously offered up on Kaggle, I figured a project on Bigfoot would fit the vibe of my small but growing portfolio.
	
I began this project with the germ of an idea, a silly, fun, easy whip this off in two days kind of idea. 
It all started with a day dream of chasing Sasquatches across the Pacific North-West via my tableau. I promptly fell down a celestial rabbit hole, and stayed there for the better part of a week! 	 


### Visit my Interactive tableau dashboards at the link below

([Find Bigfoot by Moonlight](https://public.tableau.com/views/BigFoot_16363096439910/Story1?:language=en-US&:display_count=n&:origin=viz_share_link))

![BFEDAtmp](https://user-images.githubusercontent.com/90716926/145884075-f6cca8e8-4399-4331-893e-67d7c0bfb173.png)
								
While navigating the dataset, I took special interest in the geocode tables. These tables recorded such things as the amount of cloud cover, precipitation, uv index, visibility and fractional moon light as recorded at the time of the reported sighting. 

This is where I stumbled upon my BIG QUESTION															
								
									
# The first big question was:
Could I predict the likeliest dates for Bigfeet sightings by charting the moon?	
								
						
Pretty quickly, I mean really quickly without collecting or cleaning any data I learned that yes, of course I could predict which phase of the moon is best to catch a glimpse of the elusive beast.									
I mean, people have been studying Yeti for centuries and apparently I am not the first person to ponder this question.  In this century, we have things like radar and isotopes and DNA analysis.  Of course people have peeked to see if the moon has any behavioural affects on the mighty Big Foot.									
There are plenty of sightings, over 4,947 reports across North America between 1921-2021.	
But to date: no remains, no habitats, no DNA have been confirmed as belonging to the notoriously shy bi-pedal hominid we call The Sasquatch.		

Other parts of the world have counterparts, such as the Yeti of the Himalayan Mountains and yet, no physical evidence of their existence has turned up either.									
									
With these questions in mind, I began cleaning my data. (see notes on ETL in addendum for more info on that process)									
I got through some minor hurdles, and was feeling good.  I had some idea's in mind.  I went a little deeper and thats when I recognized the BIG ISSUE.																
									
* The BIG ISSUE :
HOW to match the Lunar Cycle to Diurnal information when there is no record of TIME in the dataset?                                        									
This is where my determined nature paid off. I could have seen the issue with the time stamps and ditched the whole thing in favour of an easier, cleaner data set. But, that just isn't how I roll.  I like roads less travelled and poking mysterious things just to see what that might do. As far as I could tell, this data set was the one for me.														
									
* The BIGGER QUESTION:		
Can the DAY of a past event be determined by the fractional representation of Moon Light recorded on the day of the event?									
The answer is Yes!									
									
First, I determined DAY OF MOON by the fractional percentage of moon light on the geocode table. Because Timothy Renner's data set had the fractional representation of moon shine, I could determine the moon_day according to the amount of moon shine measured.									
Fractional amount of moon light is a more precise way to pinpoint the phase of the moon than day information as the lunar cycle varies around 30 - 24 hour periods, give or take several hours.									

I found a table that broke down the days of the month by the fractional percentage of moon shine.

I plopped those values into a column in a new sheet and did a nested IF statement to display the correct moon phase per moon_day (day 1 through 30)									
It worked!
									
#### A NOTE ON THE LUNAR CALENDAR						
The lunar cycle is approximately 30 days give or take several hours. Day 1 of the lunar cycle is the first day after the new moon.  That first day can fall anywhere within the calendar month.  For this reason, I can't use day and moon_day interchangeably nor can I use these fields on a join. 
This will cause some issues with months that have thirty one days that I will have to solve at another time.  
*For the scope of this project I am only working with the lunar month days.*  	

The *big BIGGER question* is a bit out of the scope for this project. 
Which brings me to the planning stage of CHAPTER TWO which I will touch on briefly:

# CHAPTER TWO
###### HOW To determine A DATE by Moon Light									
The new moon repeats every 29.53 days which is slightly out of sync with its rotational period around us on earth (27.32 days)									
But if you know a past New Moon Date you can determine a future Full Moon Date by determining how much time will have elapsed  between the two events and dividing that number by 29.53, the lunar period.									
I will need to use a DATEDIFF function to find the elapsed time	in order to perform the following calculation								
Days since New Moon / 29.53(lunar period) = the number of lunar periods that have passed.
I can then plot those lunar periods backwards and forwards and determine a date of a past event in this manner.
									
# Back to the task at hand
###### The Hypothesis!									
My hypothesis:  Bigfoot sightings CAN be predicted on the fractional amount of moonlight on any given day.									
The null hypothesis:  There is NO significant relationship between moonlight and Bigfoot sightings :(								
Alternative hypothesis: There IS a significant relationship between moonlight and Bigfoot sightings :)								
								
SIGNIFICANCE 								
To determine what, if any significance there is between the fractional representation of lunar light and the day of reported sightings, 		I calculated the mean, median, mode, standard deviation, variance, zscore and quartiles using google sheets	

Measures of Central Tendency								
fractional moon light	MEAN	0.3358059972						
fractional moon light	MEDIAN	0.3358059972						
fractional moon light	MODE	0.3358059972						
						
Measures of Dispersion								
fractional moon light	STD. DEV	0.2884055785						
fractional moon light	VARIANCE	0.08317777772	

QUARTILES								
fractional moon light	1st Quartile	0.0986315154		the least sightings				
fractional moon light	2nd Quartile	0.196357416						
fractional moon light	3rd quartile	0.2818494667						
fractional moon light	4th quartile	0.3358059972		The most sightings	

								
# Full Moon Light								
The highest recorded value in the data set, is 1. 								

On the 4,395th day of the data set, we find the single sighting to have occured during a full moon.								
> We know it was a full moon because the fractional moon light value was recorded as 1, and 1 is the highest possible value which only happens under the conditions of a full moon.
> 								
The sighting took place downriver of Telogia Creek in Wakulla County, Florida.								
It's interesting to note even though there was a full moon that winter night, there was 98% cloud cover.								
								
# This calls for a Z-test								
(the high value ) - (the mean) / std.deviation = zscore								
In this case as follows: 1.0-0.3358059972/.2884055785=zscore								
if the value of z is greater than 1.96 or less than -1.96, the null hypothesis is rejected. 								
The null hypothesis states that there is little to no significance between the two variables								
								
###### The Z-Test								
1.0-0.3358059972/.2884055785=zscore								
ZScore =	2.302985976							
###### Outcome is Very Significant, the alternative hypothesis is accepted!						
								
# Lets look at some visualizations							
								
![Mean of moon shine per moon phase](https://github.com/slaing77/Finding-Bigfoot_by_moonlight/blob/fbd2728ee92b7b7977841a23dab3dbd53bf60d67/docs/images/1.%20Mean%20of%20Moon%20Shine%20per%20Moon%20Phase.png)

![Mean of moon shine per lunar day](https://github.com/slaing77/Finding-Bigfoot_by_moonlight/blob/fbd2728ee92b7b7977841a23dab3dbd53bf60d67/docs/images/2.%20Mean%20of%20Moon%20SHine%20per%20Lunar%20Day.png)

![Mean of moon shine per sighting](https://github.com/slaing77/Finding-Bigfoot_by_moonlight/blob/fbd2728ee92b7b7977841a23dab3dbd53bf60d67/docs/images/3.%20Average%20Moon%20Shine%20per%20Sighting%20.png)
									
								
1. We can see the fraction of moon light remains constant throughout the lunar phases.								
2. By confirming how perfectly the lunar days match to the phases of the moon, we can confirm the new moon falls around the 20th of each calendar month and the full moon falls on or around the 5th. * Note: these dates move incrementally throughout time as a lunar month is approximately 30 days give or take a few hours in either direction.*								
								
3. We can also see that the average fraction of moon shine per sighting remains between .44 and .54								
And can predict the most sightings will fall during the first quarter phase and the waning gibbous phase								
We can also predict the least sightings will take place outside of this range.								
								
Looking at our quartiles, we can determine that the least sightings occur during the periods with the least light, on the new moon								
Remembering what we learned about the highest moon light value is '1' = the full moon.
That only one sighting ever occurred on the full moon and, that was during a winter night with 98% cloud cover. 					
We know the brightest and the darkest time of the lunar month are the least likely times to sneak a peek of our hairy friend.	

# Closing with a mystery

One thing that caught my eye were two time periods.  The late 70's early 80's had a small bump in reported sightings that mirror a much larger bump in the early '00's as you can see below.  


![Sightings over time](https://github.com/slaing77/Finding-Bigfoot_by_moonlight/blob/fbd2728ee92b7b7977841a23dab3dbd53bf60d67/docs/images/Sightings%20over%20time.png)

I found this intriguing and decided to see if media had anything to do with the jumps. Thinking of the infamous Patterson-Gimlin film. I went to wikipedia and learned it was first released into the wild in 1967. A full decade before the time period in question.  

By <a href="//en.wikipedia.org/wiki/Patterson%E2%80%93Gimlin_film" title="Patterson–Gimlin film">Patterson–Gimlin film</a>, Fair use, <a href="https://en.wikipedia.org/w/index.php?curid=434396">Link</a>

![Patterson–Gimlin_film_frame_352](https://user-images.githubusercontent.com/90716926/145883697-88263654-1b6a-4e16-87e7-9c89eb23c528.jpg)

My mind then scurried off to Harry and the Henderson's.  When I checked that title, I saw the series didn't air until the late 80's.  Outside of the time bump.  
I realized I was on the precipice of yet another rabbit hole when I began searching the IMDB for terms like Bigfoot, Sasquatch and Yeti looking for some kind of star powered box office hit to explain the uptick in sightings.  I came a way with a handful of B movies, none with a rating higher than 5.5, but my google searched revealed something very intriguing indeed.

### Alleged Bigfoot attack in Ape Canyon
([Alleged Bigfoot attack in Ape Canyon](https://en.wikipedia.org/wiki/Ape_Canyon#Alleged_Bigfoot_attack))
			
On July 16, 1924 the Oregonian reported on an alleged violent encounter ‘between a group of miners and a group of  Ape men”, resulting in the death of an ape man, by bullet wound.

Nearly sixty years later a man named William Halliday born only two years after the infamous tale was printed in the Oregonian,  appeared to have some inside knowledge on this event. In 1983, now the director of the Western Speleological Survey,Halliday released a pamphlet called **‘Ape Cave and the Mount Saint Helens Apes’**  wherein he outed the real assailants as local youth throwing rocks from the canyons above.  The sun light was behind them, concealing their features and throwing wicked shadows. Thus an urban legend was born.
<p>I still have no insight as to what caused these two bumps in reported activity, but I do wonder if the uptick in BigFoot interest created a sense of urgency in William to set the record straight. </p>

As a last note I came across this interesting tidbit ([FBI release files from 1970's on hair samples](https://youtu.be/1E3XID7z8ZQ))
### Spoiler Alert:
93 year old Peter Byrne, Bigfoot enthusiast finally finds out what happened to the sample of hair he sent into the FBI in 1976.
The results had been 'lost' in the mail for decades. When the FBI recently released their own Bigfoot file, they revealed Mr. Byrnes sample had been determined to belong to some type of deer.

I bring this up because one astonishing witness account in the data set mirrors Mr. Byrnes experience.
The account is quite long and detailed.  Report #60 is out of Skagit county, WA and was logged in 1994, the date of the actual sighting is missing and therefore this account is not included in my population for analysis. The report discusses multiple sightings over a period of time.  This entry focuses on two recluse ranchers (brothers) and attacks on their livestock, witness accounts of bi-pedal hairy beasts and the collection of dung which was sent off to the lab for analysis.  

The results were, unlike my hypothesis ... **inconclusive.**		
					
								
								
								
								
								
